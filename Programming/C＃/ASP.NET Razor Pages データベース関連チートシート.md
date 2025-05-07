
## Migration コマンド

bash

```bash
# Migration の作成
dotnet ef migrations add InitialCreate

# 特定の DbContext を指定
dotnet ef migrations add InitialCreate --context ApplicationDbContext

# Migration の削除
dotnet ef migrations remove

# データベースの更新
dotnet ef database update

# 特定の Migration まで更新
dotnet ef database update AddProductTable

# Migration のスクリプト生成
dotnet ef migrations script

# スキーマの表示
dotnet ef dbcontext info

# DbContext のリバースエンジニアリング
dotnet ef dbcontext scaffold "Server=myserver;Database=mydb;User Id=myuser;Password=mypass;" Microsoft.EntityFrameworkCore.SqlServer -o Models
```

## PageModel でのデータアクセス

csharp

```csharp
public class IndexModel : PageModel
{
    private readonly ApplicationDbContext _context;
    
    public IndexModel(ApplicationDbContext context)
    {
        _context = context;
    }
    
    public IList<Customer> Customers { get; set; }
    
    public async Task OnGetAsync()
    {
        // 基本的な取得
        Customers = await _context.Customers.ToListAsync();
        
        // フィルタリング
        Customers = await _context.Customers
            .Where(c => c.IsActive)
            .ToListAsync();
            
        // 関連データの取得 (Include)
        Customers = await _context.Customers
            .Include(c => c.Orders)
            .ToListAsync();
            
        // 並べ替え
        Customers = await _context.Customers
            .OrderBy(c => c.LastName)
            .ThenBy(c => c.FirstName)
            .ToListAsync();
            
        // ページング
        int pageSize = 10;
        int pageIndex = 1;
        Customers = await _context.Customers
            .Skip((pageIndex - 1) * pageSize)
            .Take(pageSize)
            .ToListAsync();
    }
}
```