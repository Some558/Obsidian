# Razor Pagesにおけるnull許容・非許容のベストプラクティス

Razor Pagesでのnull許容・非許容の扱いは多くの開発者が悩まされる問題です。C# 8.0以降のNullable Reference Types機能と、ASP.NET CoreのPageModelのライフサイクルが絡み合うことで複雑になります。以下に、実践的なベストプラクティスをまとめます。

## 1. プロジェクト設定の理解

### Nullableの設定

xml

```xml
<!-- .csproj ファイル -->
<PropertyGroup>
  <Nullable>enable</Nullable> <!-- 非null参照型を有効化 -->
</PropertyGroup>
```

この設定により:

- 全ての参照型は**デフォルトで非null**となる
- null許容にするには**明示的に `?` を付ける**必要がある
- 初期化されていない非null参照型に対して**警告**が表示される

## 2. モデルクラスでのnull扱いの基本原則

### 2.1 エンティティ（データモデル）クラス

csharp

```csharp
public class Product
{
    public int Id { get; set; }
    
    // 必須プロパティ
    [Required]
    public string Name { get; set; } = string.Empty; // 初期値を設定
    
    // null許容プロパティ
    public string? Description { get; set; }
    
    // 関連エンティティ（外部キーあり）
    public int? CategoryId { get; set; } // null許容なら外部キーもnull許容に
    public Category? Category { get; set; } // 関連も同様に
    
    // または必須の関連
    public int SupplierId { get; set; }
    public Supplier Supplier { get; set; } = null!; // 後で初期化されることを示す
}
```

**原則**:

- 必須の単純型プロパティには**初期値を設定**する
- 必須の参照型プロパティ（文字列など）には**初期値に空の値を設定**する
- null許容プロパティは**明示的に `?` を付ける**
- EFの関連は**外部キーとナビゲーションプロパティの整合性**を保つ
- 必須の関連プロパティには `= null!` を使用して「後で初期化される」ことを示す

### 2.2 PageModelクラス

csharp

```csharp
public class EditModel : PageModel
{
    private readonly ApplicationDbContext _context;
    
    // DIで初期化されるサービス
    public EditModel(ApplicationDbContext context)
    {
        _context = context;
    }
    
    // ページ読み込み時に初期化されるプロパティ
    public Product? Product { get; set; } // null許容で定義
    
    // フォーム送信時にバインドされるプロパティ
    [BindProperty]
    public InputModel Input { get; set; } = new InputModel(); // 常に初期化
    
    // フォーム入力モデル
    public class InputModel
    {
        [Required]
        public string Name { get; set; } = string.Empty;
        
        public string? Description { get; set; }
        
        [Range(1, 1000)]
        public decimal Price { get; set; }
        
        public int? CategoryId { get; set; }
    }
}
```

**原則**:

- DIで初期化されるサービスはコンストラクタで確実に設定
- ページ読み込み時に初期化されるプロパティは**null許容型**で定義するか、**ロード前に初期化**
- フォームバインディング用のプロパティは**常に初期化**（例: `= new InputModel()`）
- フォーム入力モデルは**入力の必須性に応じた型**を選択

## 3. シナリオ別のベストプラクティス

### 3.1 ページロード時のモデルロード

csharp

```csharp
public async Task<IActionResult> OnGetAsync(int? id)
{
    if (id == null)
    {
        return NotFound();
    }

    // 明示的なIncludeとnullチェック
    var product = await _context.Products
        .Include(p => p.Category)
        .FirstOrDefaultAsync(p => p.Id == id);
        
    if (product == null)
    {
        return NotFound();
    }
    
    Product = product;
    Input = new InputModel
    {
        Name = product.Name,
        Description = product.Description,
        Price = product.Price,
        CategoryId = product.CategoryId
    };
    
    return Page();
}
```

**原則**:

- パラメータが**必須の場合は非null型**、オプションの場合は**null許容型**で定義
- クエリ結果は**常にnullチェック**する
- ページモデルのプロパティに代入する前に**nullチェック**する

### 3.2 フォーム送信とモデルバインディング

csharp

```csharp
public async Task<IActionResult> OnPostAsync()
{
    if (!ModelState.IsValid)
    {
        // カテゴリ一覧などの再取得が必要
        await LoadSelectListsAsync();
        return Page();
    }

    // DBから既存のエンティティを取得
    var product = await _context.Products.FindAsync(Input.Id);
    if (product == null)
    {
        return NotFound();
    }
    
    // 入力値を既存エンティティにマッピング
    product.Name = Input.Name;
    product.Description = Input.Description;
    product.Price = Input.Price;
    product.CategoryId = Input.CategoryId;
    
    try
    {
        await _context.SaveChangesAsync();
        return RedirectToPage("./Index");
    }
    catch (DbUpdateConcurrencyException)
    {
        if (!ProductExists(Input.Id))
        {
            return NotFound();
        }
        else
        {
            throw;
        }
    }
}
```

**原則**:

- モデルバインディングエラー時は**必要なデータを再取得**する
- DBから取得したエンティティは**常にnullチェック**する
- 更新時は**既存エンティティに値をマッピング**する（新しいインスタンスを作らない）

### 3.3 SelectListなどの静的データの取得

csharp

```csharp
// クラスレベルで宣言
public SelectList? CategoryList { get; set; }

// 読み込み前に初期化するメソッド
private async Task LoadSelectListsAsync()
{
    // カテゴリ一覧を取得してSelectListを作成
    CategoryList = new SelectList(
        await _context.Categories.ToListAsync(),
        "Id",
        "Name",
        Input?.CategoryId // 現在の選択値（nullの可能性あり）
    );
}

// OnGetAsync内で呼び出し
public async Task<IActionResult> OnGetAsync()
{
    await LoadSelectListsAsync();
    return Page();
}

// OnPostAsync内でもエラー時に呼び出し
public async Task<IActionResult> OnPostAsync()
{
    if (!ModelState.IsValid)
    {
        await LoadSelectListsAsync();
        return Page();
    }
    // ...
}
```

**原則**:

- SelectListなどの補助データは**null許容型**で定義するか**常に初期化**
- ページ読み込みとフォーム送信の**両方で初期化メソッドを呼び出す**
- 初期化ロジックは**共通のメソッドに抽出**する

## 4. Entity Frameworkとナビゲーションプロパティ

### 4.1 DbContext設定での関連の明示

csharp

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    // 必須の関連
    modelBuilder.Entity<Product>()
        .HasOne(p => p.Supplier)
        .WithMany(s => s.Products)
        .HasForeignKey(p => p.SupplierId)
        .IsRequired();
    
    // オプショナルな関連
    modelBuilder.Entity<Product>()
        .HasOne(p => p.Category)
        .WithMany(c => c.Products)
        .HasForeignKey(p => p.CategoryId)
        .IsRequired(false);
}
```

**原則**:

- 関連の必須性を**データベースレベルで明示的に設定**
- コードの型とデータベースの制約を**一致させる**

### 4.2 Includeの使用

csharp

```csharp
// null許容演算子で警告を回避
var products = await _context.Products
    .Include(p => p.Category!)
    .Include(p => p.Supplier!)
    .ToListAsync();

// 代替アプローチ: 文字列ベースのInclude
var products = await _context.Products
    .Include("Category")
    .Include("Supplier")
    .ToListAsync();
```

**原則**:

- 必須の関連を含める場合は**null非許容演算子(`!`)**を使用
- オプショナルな関連の場合は**通常のInclude**を使用し、使用時にnullチェック
- または型の安全性を犠牲にして**文字列ベースのInclude**を使用

## 5. コード分析とコンパイラ警告への対応

### 5.1 エディターコンフィグでの設定

editorconfig

```editorconfig
# .editorconfig
[*.cs]
# 特定の警告を調整
dotnet_diagnostic.CS8618.severity = suggestion # Non-nullable property is uninitialized
```

**原則**:

- 特定のパターンで頻発する警告は**コンフィグファイルで調整**する
- 警告を無視するのではなく**重要度を下げる**ことで気付きやすくする

### 5.2 プラグマによる警告の抑制

csharp

```csharp
#pragma warning disable CS8618 // Non-nullable field must contain a non-null value
public DbSet<Product> Products { get; set; }
#pragma warning restore CS8618
```

**原則**:

- プラグマは**最小限の範囲**に限定して使用
- 必ず**警告を復元**するコードを含める
- 抑制の**理由をコメント**で明記する

## 6. 共通パターンとアンチパターン

### ベストプラクティス

1. **初期化の明確化**:
    
    csharp
    
    ```csharp
    // 後で初期化される非null参照型
    public Category Category { get; set; } = null!;
    
    // 常に値を持つべき参照型
    public string Name { get; set; } = string.Empty;
    
    // null許容の参照型
    public string? Description { get; set; }
    ```
    
2. **PageModelのプロパティ初期化**:
    
    csharp
    
    ```csharp
    // フォーム入力用プロパティは常に初期化
    [BindProperty]
    public InputModel Input { get; set; } = new();
    
    // コレクションは空のコレクションで初期化
    public List<SelectListItem> Categories { get; set; } = new();
    ```
    
3. **null条件演算子とnull合体演算子の活用**:
    
    csharp
    
    ```csharp
    // null安全なアクセス
    var categoryName = product.Category?.Name ?? "カテゴリなし";
    ```
    

### アンチパターン

1. **空のコンストラクタでの初期化の省略**:
    
    csharp
    
    ```csharp
    // 良くない例
    public class EditModel : PageModel
    {
        // 初期化されていない非nullプロパティ
        public List<Product> Products { get; set; }
        
        public EditModel() { /* 初期化なし */ }
    }
    ```
    
2. **後で初期化される値に対する型の不一致**:
    
    csharp
    
    ```csharp
    // 良くない例 - null許容として定義しつつnullチェックなしで使用
    public Product? Product { get; set; }
    
    public void ProcessProduct()
    {
        var name = Product.Name; // Productがnullの可能性あり
    }
    ```
    
3. **Includeでのナビゲーションプロパティの不適切な扱い**:
    
    csharp
    
    ```csharp
    // 良くない例 - 警告が発生
    var products = _context.Products.Include(p => p.Category).ToList();
    
    // より良い例
    var products = _context.Products.Include(p => p.Category!).ToList();
    // または
    var products = _context.Products.Include("Category").ToList();
    ```
    

## 7. Razor Pagesのライフサイクルを考慮したnull処理

### 7.1 OnGetAsyncでのデータロード

csharp

```csharp
public async Task<IActionResult> OnGetAsync()
{
    // コレクションは取得前に初期化されている
    Products = await _context.Products.ToListAsync();
    
    // 単一エンティティはnullの可能性あり
    var product = await _context.Products.FirstOrDefaultAsync(p => p.Featured);
    FeaturedProduct = product; // null許容型で定義されている場合はOK
    
    // バインディング用モデルは値をコピー
    if (product != null)
    {
        Input = new InputModel
        {
            Id = product.Id,
            Name = product.Name,
            // ...他のプロパティ
        };
    }
    
    return Page();
}
```

### 7.2 OnPostAsyncでのバインディングとバリデーション

csharp

```csharp
public async Task<IActionResult> OnPostAsync()
{
    // ModelStateが無効な場合は再表示用データを読み込む
    if (!ModelState.IsValid)
    {
        // 必要なデータを再取得（SelectListなど）
        await LoadFormDataAsync();
        return Page();
    }
    
    // 既存エンティティの更新（編集の場合）
    if (Input.Id > 0)
    {
        var existingProduct = await _context.Products.FindAsync(Input.Id);
        if (existingProduct == null)
        {
            return NotFound();
        }
        
        // マッピング
        _context.Entry(existingProduct).CurrentValues.SetValues(Input);
        await _context.SaveChangesAsync();
    }
    else
    {
        // 新規作成
        var newProduct = new Product
        {
            Name = Input.Name,
            Description = Input.Description,
            // ...他のプロパティ
        };
        
        _context.Products.Add(newProduct);
        await _context.SaveChangesAsync();
    }
    
    return RedirectToPage("./Index");
}
```

## 8. 総合的なnull処理戦略

### 8.1 プロジェクトレベルでの戦略

1. **一貫したnull許容戦略を確立**:
    - プロジェクト全体で`<Nullable>enable</Nullable>`を有効に
    - null参照例外を避けるため、設計時に常にnull可能性を考慮
2. **適切な初期化パターン**:
    - 必須参照型: 初期値を設定（`= string.Empty`、`= new List<T>()`など）
    - 後で初期化される参照型: `= null!`でマーク
    - オプショナル参照型: `?`付きで明示的にnull許容に
3. **Razor Pagesライフサイクル**:
    - PageModelプロパティの役割による適切な型選択
    - OnGet/OnPostのそれぞれで必要なデータロードを理解

### 8.2 実践的なチェックリスト

✅ **データモデル**:

- [ ]  必須の文字列プロパティに初期値を設定（`= string.Empty`）
- [ ]  必須のコレクションプロパティを初期化（`= new List<T>()`）
- [ ]  オプショナルなプロパティに`?`を付加
- [ ]  ナビゲーションプロパティと外部キーの一貫性を確保

✅ **PageModel**:

- [ ]  DIで注入されるサービスはコンストラクタで設定
- [ ]  フォーム送信用の[BindProperty]は初期化
- [ ]  SelectListなどの補助データを適切に初期化
- [ ]  OnGetとOnPostの両方でデータロードを処理

✅ **バリデーション**:

- [ ]  ModelState.IsValidチェック後の必要なデータ再取得
- [ ]  参照型プロパティのnullチェック
- [ ]  コレクションの空チェック（`.Any()`）
- [ ]  レコード存在確認前の主キー値チェック

✅ **Entity Framework**:

- [ ]  Includeでのナビゲーションプロパティの適切な扱い
- [ ]  DbContext設定での関連の明示
- [ ]  外部キーnull状態の一貫した処理

## 結論

ASP.NET Core Razor PagesでC# 8.0以降のNullable Reference Typesを使用する場合は、モデルのライフサイクルとnull許容性を十分に理解することが重要です。適切なパターンを一貫して適用することで、コンパイラ警告を減らしながら型安全性を高めることができます。

最も重要なのは、「このプロパティはnullになり得るか？」という問いに対して正直に答え、コードの型がその現実を反映していることを確認することです。初期化のタイミングとライフサイクルを理解し、その知識に基づいて適切な型と初期化パターンを選択することが、エラーを防ぎ保守性の高いコードにつながります。