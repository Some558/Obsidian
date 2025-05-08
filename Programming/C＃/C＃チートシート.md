# C# Syntax Cheatsheet (.NET 8)

## 基本構文

### コメント

```csharp
// 1行コメント
/* 複数行
   コメント */
/// XMLドキュメンテーションコメント
```

### データ型

```csharp
// 値型
bool      // True/False
byte      // 8ビット符号なし整数 (0～255)
sbyte     // 8ビット符号付き整数 (-128～127)
char      // 16ビット Unicode文字
decimal   // 128ビット高精度小数 (財務計算向け)
double    // 64ビット倍精度浮動小数点
float     // 32ビット単精度浮動小数点
int       // 32ビット符号付き整数
uint      // 32ビット符号なし整数
long      // 64ビット符号付き整数
ulong     // 64ビット符号なし整数
short     // 16ビット符号付き整数
ushort    // 16ビット符号なし整数

// 参照型
string    // 文字列
object    // すべての型の基底クラス
dynamic   // 動的型

// その他
var       // 型推論（コンパイル時に決定）
nint      // ネイティブサイズの整数 (IntPtr)
nuint     // ネイティブサイズの符号なし整数 (UIntPtr)
```

### 変数宣言

```csharp
int x = 10;
var y = 20;  // 型推論
const double Pi = 3.14159;  // 定数
readonly int ReadOnlyField;  // 読み取り専用フィールド
```

### リテラル

```csharp
// 数値リテラル
int decimal = 42;
int hex = 0x2A;      // 16進数
int binary = 0b101010; // 2進数
long bigNumber = 1_000_000;  // 数値区切り文字

// 文字列リテラル
string s1 = "通常の文字列";
string s2 = @"逐語的文字列
複数行可能"; 
string s3 = $"補間文字列 {x}";  // 変数の埋め込み
string s4 = """
    JSONなどの複数行文字列（.NET 7以降）
    "引用符"も簡単に扱える
    """;
```

## 演算子

### 算術演算子

```csharp
int a = 10, b = 3;
int sum = a + b;      // 加算
int diff = a - b;     // 減算
int product = a * b;  // 乗算
int quotient = a / b; // 除算
int remainder = a % b; // 剰余
```

### 比較演算子

```csharp
bool equal = (a == b);        // 等しい
bool notEqual = (a != b);     // 等しくない
bool greater = (a > b);       // より大きい
bool less = (a < b);          // より小さい
bool greaterEqual = (a >= b); // 以上
bool lessEqual = (a <= b);    // 以下
```

### 論理演算子

```csharp
bool and = (a > 0 && b > 0);  // AND
bool or = (a > 0 || b > 0);   // OR
bool not = !(a > 0);          // NOT
```

### ビット演算子

```csharp
int bitwiseAnd = a & b;   // ビットAND
int bitwiseOr = a | b;    // ビットOR
int bitwiseXor = a ^ b;   // ビットXOR
int bitwiseNot = ~a;      // ビット反転
int leftShift = a << 2;   // 左シフト
int rightShift = a >> 1;  // 右シフト
```

### 代入演算子

```csharp
x += 5;   // x = x + 5 と同じ
x -= 5;   // x = x - 5 と同じ
x *= 5;   // x = x * 5 と同じ
x /= 5;   // x = x / 5 と同じ
x %= 5;   // x = x % 5 と同じ
x &= 5;   // x = x & 5 と同じ
x |= 5;   // x = x | 5 と同じ
x ^= 5;   // x = x ^ 5 と同じ
x <<= 1;  // x = x << 1 と同じ
x >>= 1;  // x = x >> 1 と同じ
```

### その他の演算子

```csharp
x++;  // インクリメント
x--;  // デクリメント
?:    // 三項演算子 (条件 ? 真の場合 : 偽の場合)
??    // null合体演算子
?.    // null条件演算子
=     // 代入
=>    // ラムダ演算子
is    // 型チェック
as    // 型変換（失敗時null）
sizeof // 型のサイズを取得
typeof // 型の情報を取得
new    // オブジェクト生成
```

### パターンマッチング

```csharp
// is パターン
if (obj is string s) { /* sを使用 */ }

// switch 式
string message = x switch
{
    0 => "ゼロ",
    1 => "イチ",
    _ => "その他"
};

// リストパターン
if (list is [var first, _, ..])
{
    // first は最初の要素, .. は残りの要素
}

// プロパティパターン
if (person is { Name: "John", Age: > 18 })
{
    // Nameが"John"でAgeが18より大きい
}
```

## 制御構造

### 条件分岐

```csharp
// if文
if (x > 0)
{
    // 真の場合の処理
}
else if (x < 0)
{
    // 別の条件の処理
}
else
{
    // それ以外の処理
}

// switch文
switch (day)
{
    case DayOfWeek.Monday:
        Console.WriteLine("月曜日");
        break;
    case DayOfWeek.Tuesday:
    case DayOfWeek.Wednesday:
        Console.WriteLine("火曜または水曜");
        break;
    default:
        Console.WriteLine("その他の曜日");
        break;
}

// 三項演算子
string status = (age >= 18) ? "成人" : "未成年";
```

### ループ

```csharp
// for文
for (int i = 0; i < 10; i++)
{
    // 繰り返し処理
}

// foreach文
foreach (var item in collection)
{
    // 各要素に対する処理
}

// while文
while (condition)
{
    // 条件が真の間、繰り返し
}

// do-while文
do
{
    // 最低1回は実行され、条件が真の間繰り返し
} while (condition);
```

### ジャンプステートメント

```csharp
break;     // ループや switch を抜ける
continue;  // ループの次の繰り返しへ
return;    // メソッドから戻る
goto label; // 指定したラベルへジャンプ
label:      // goto のターゲット
```

## メソッド

### メソッド定義

```csharp
// 基本的なメソッド
void DoSomething()
{
    // コード
}

// パラメータと戻り値を持つメソッド
int Add(int a, int b)
{
    return a + b;
}

// 式形式のメソッド（1行で記述）
int Multiply(int a, int b) => a * b;

// オプショナルパラメータ
void Display(string message, bool isUpperCase = false)
{
    // isUpperCaseはオプション
}

// 名前付き引数
Display(isUpperCase: true, message: "テスト");

// 可変長引数
int Sum(params int[] numbers)
{
    int total = 0;
    foreach (var number in numbers)
    {
        total += number;
    }
    return total;
}

// タプル戻り値
(int Min, int Max) GetRange(int[] numbers)
{
    return (numbers.Min(), numbers.Max());
}

// out パラメータ
bool TryParse(string input, out int result)
{
    // resultに値を設定する必要がある
    result = 0;
    return int.TryParse(input, out result);
}

// ref パラメータ
void Swap(ref int a, ref int b)
{
    int temp = a;
    a = b;
    b = temp;
}

// in パラメータ（読み取り専用参照）
void Process(in LargeStruct data)
{
    // dataは変更できない
}
```

### ローカル関数

```csharp
void ProcessData()
{
    // ローカル関数（メソッド内で定義される関数）
    int CalculateValue(int input)
    {
        return input * 2;
    }
    
    int result = CalculateValue(10);
}
```

## クラスとオブジェクト

### クラス定義

```csharp
// 基本的なクラス
public class Person
{
    // フィールド
    private string _name;
    private int _age;
    
    // プロパティ
    public string Name
    {
        get { return _name; }
        set { _name = value; }
    }
    
    // 自動実装プロパティ
    public int Age { get; set; }
    
    // 読み取り専用プロパティ
    public bool IsAdult => Age >= 18;
    
    // コンストラクタ
    public Person(string name, int age)
    {
        _name = name;
        _age = age;
    }
    
    // メソッド
    public void Introduce()
    {
        Console.WriteLine($"私は{Name}、{Age}歳です。");
    }
    
    // オーバーロードされたメソッド
    public void Introduce(string greeting)
    {
        Console.WriteLine($"{greeting}、私は{Name}です。");
    }
    
    // 静的メソッド
    public static Person CreateAdult(string name)
    {
        return new Person(name, 18);
    }
    
    // デストラクタ（ファイナライザ）
    ~Person()
    {
        // リソースのクリーンアップ
    }
}
```

### オブジェクト初期化

```csharp
// コンストラクタでの初期化
Person person1 = new Person("John", 30);

// オブジェクト初期化子
Person person2 = new Person
{
    Name = "Alice",
    Age = 25
};

// var と new の簡略構文（.NET 6以降）
var person3 = new Person("Bob", 22);

// ターゲットタイプ new 式（.NET 5以降）
Person person4 = new("Charlie", 35);
```

### 継承

```csharp
// 基底クラス
public class Animal
{
    public string Name { get; set; }
    
    public virtual void MakeSound()
    {
        Console.WriteLine("動物の鳴き声");
    }
}

// 派生クラス
public class Dog : Animal
{
    public string Breed { get; set; }
    
    // メソッドのオーバーライド
    public override void MakeSound()
    {
        Console.WriteLine("ワンワン！");
    }
    
    // 基底クラスのメソッド呼び出し
    public void MakeSoundTwice()
    {
        base.MakeSound();
        MakeSound();
    }
}
```

### インターフェイス

```csharp
// インターフェイス定義
public interface IMovable
{
    void Move(int x, int y);
    int Speed { get; set; }
    
    // デフォルト実装（.NET Standard 2.1以降）
    void Stop() => Console.WriteLine("停止しました");
}

// インターフェイスの実装
public class Car : IMovable
{
    public int Speed { get; set; }
    
    public void Move(int x, int y)
    {
        Console.WriteLine($"({x}, {y})に移動");
    }
}

// 複数インターフェイスの実装
public class Robot : IMovable, IDisposable
{
    public int Speed { get; set; }
    
    public void Move(int x, int y) { /* 実装 */ }
    
    public void Dispose() { /* リソース解放 */ }
}
```

### 抽象クラス

```csharp
// 抽象クラス
public abstract class Shape
{
    public string Color { get; set; }
    
    // 抽象メソッド（実装なし）
    public abstract double CalculateArea();
    
    // 通常のメソッド
    public void SetColor(string color)
    {
        Color = color;
    }
}

// 抽象クラスを継承
public class Circle : Shape
{
    public double Radius { get; set; }
    
    // 抽象メソッドの実装
    public override double CalculateArea()
    {
        return Math.PI * Radius * Radius;
    }
}
```

### シールドクラスとメソッド

```csharp
// シールドクラス（継承不可）
public sealed class Utility
{
    // ユーティリティメソッド
}

// シールドメソッド
public class BaseClass
{
    public virtual void Method() { }
}

public class DerivedClass : BaseClass
{
    // このメソッドはこれ以上オーバーライドできない
    public sealed override void Method() { }
}
```

### 静的クラス

```csharp
// 静的クラス（インスタンス化不可）
public static class MathHelper
{
    // 静的メソッド
    public static double CalculateCircumference(double radius)
    {
        return 2 * Math.PI * radius;
    }
    
    // 静的プロパティ
    public static double Pi => 3.14159;
}
```

### 拡張メソッド

```csharp
// 拡張メソッド用の静的クラス
public static class StringExtensions
{
    // string型の拡張メソッド
    public static bool IsNullOrEmpty(this string str)
    {
        return string.IsNullOrEmpty(str);
    }
    
    // 使用例: "hello".IsNullOrEmpty()
}
```

## ジェネリクス

### ジェネリッククラス

```csharp
// ジェネリッククラス
public class Stack<T>
{
    private T[] _items;
    private int _count;
    
    public void Push(T item) { /* 実装 */ }
    public T Pop() { /* 実装 */ return _items[--_count]; }
}

// 使用例
var intStack = new Stack<int>();
var stringStack = new Stack<string>();
```

### ジェネリックメソッド

```csharp
// ジェネリックメソッド
public T Max<T>(T a, T b) where T : IComparable<T>
{
    return a.CompareTo(b) > 0 ? a : b;
}

// 使用例
int maxInt = Max<int>(5, 10);
string maxString = Max("apple", "banana");
```

### 型制約

```csharp
// 型制約の例
class DataStore<T> where T : class, new()
{
    // Tは参照型で、パラメータなしコンストラクタを持つ必要がある
}

// 複数の型パラメータと制約
class KeyValueProcessor<TKey, TValue>
    where TKey : struct
    where TValue : class, IComparable<TValue>
{
    // TKeyは値型、TValueは参照型でIComparable<TValue>を実装している必要がある
}
```

### 共変性と反変性

```csharp
// 共変性（out）- より派生した型を返せる
interface IProducer<out T>
{
    T Produce();
}

// 反変性（in）- より基底の型を受け入れられる
interface IConsumer<in T>
{
    void Consume(T item);
}
```

## コレクション

### 配列

```csharp
// 配列宣言と初期化
int[] numbers = new int[5];
int[] initializedNumbers = new int[] { 1, 2, 3, 4, 5 };
int[] shortSyntax = { 1, 2, 3, 4, 5 };

// 多次元配列
int[,] matrix = new int[3, 4];
int[,] initializedMatrix = { 
    { 1, 2, 3, 4 }, 
    { 5, 6, 7, 8 }, 
    { 9, 10, 11, 12 } 
};

// ジャグ配列（不規則な配列）
int[][] jaggedArray = new int[3][];
jaggedArray[0] = new int[] { 1, 2, 3 };
jaggedArray[1] = new int[] { 4, 5 };
jaggedArray[2] = new int[] { 6, 7, 8, 9 };
```

### リスト

```csharp
// リスト宣言と初期化
List<int> numbers = new List<int>();
List<int> initializedList = new List<int> { 1, 2, 3, 4, 5 };

// 操作
numbers.Add(1);      // 要素追加
numbers.AddRange(new[] { 2, 3, 4 });  // 複数要素追加
numbers.Insert(0, 0);  // 指定位置に挿入
numbers.Remove(3);     // 要素削除
numbers.RemoveAt(0);   // 指定位置の要素削除
int count = numbers.Count;  // 要素数
bool contains = numbers.Contains(5);  // 含まれるか
int indexOf = numbers.IndexOf(4);     // インデックス取得
```

### 辞書

```csharp
// 辞書宣言と初期化
Dictionary<string, int> ages = new Dictionary<string, int>();
Dictionary<string, int> initializedDict = new Dictionary<string, int>
{
    ["John"] = 30,
    ["Alice"] = 25
};

// 操作
ages["Bob"] = 40;  // 追加または更新
bool containsKey = ages.ContainsKey("John");  // キー存在確認
ages.Remove("Alice");  // 削除
ages.TryGetValue("Bob", out int bobAge);  // 安全に値取得
foreach (var pair in ages)
{
    Console.WriteLine($"{pair.Key}: {pair.Value}");
}
```

### セット

```csharp
// HashSet宣言と初期化
HashSet<string> names = new HashSet<string>();
HashSet<string> initializedSet = new HashSet<string> { "John", "Alice", "Bob" };

// 操作
names.Add("Charlie");  // 要素追加
names.Remove("Alice");  // 要素削除
bool contains = names.Contains("Bob");  // 含まれるか
names.UnionWith(new[] { "David", "Eve" });  // 和集合
names.IntersectWith(otherSet);  // 積集合
```

### スタックとキュー

```csharp
// スタック（LIFO）
Stack<string> stack = new Stack<string>();
stack.Push("first");
stack.Push("second");
string item = stack.Pop();  // "second"

// キュー（FIFO）
Queue<string> queue = new Queue<string>();
queue.Enqueue("first");
queue.Enqueue("second");
string queueItem = queue.Dequeue();  // "first"
```

### IEnumerable と LINQ

```csharp
// IEnumerable
IEnumerable<int> numbers = Enumerable.Range(1, 10);

// LINQ
var evenNumbers = numbers.Where(n => n % 2 == 0);
var squares = numbers.Select(n => n * n);
var sum = numbers.Sum();
var average = numbers.Average();
var ordered = numbers.OrderByDescending(n);
var first = numbers.First();
var any = numbers.Any(n => n > 5);
var all = numbers.All(n => n > 0);

// クエリ構文
var query = from n in numbers
            where n % 2 == 0
            orderby n
            select n * n;
```

## 例外処理

### 基本的な例外処理

```csharp
try
{
    // 例外が発生する可能性があるコード
    int result = Divide(10, 0);
}
catch (DivideByZeroException ex)
{
    // 特定の例外をキャッチ
    Console.WriteLine($"ゼロ除算エラー: {ex.Message}");
}
catch (Exception ex)
{
    // あらゆる例外をキャッチ
    Console.WriteLine($"エラー: {ex.Message}");
}
finally
{
    // 例外の有無にかかわらず実行される
    Console.WriteLine("常に実行");
}
```

### 例外のスロー

```csharp
public int Divide(int a, int b)
{
    if (b == 0)
    {
        throw new DivideByZeroException("ゼロで割ることはできません");
    }
    return a / b;
}
```

### カスタム例外

```csharp
// カスタム例外クラス
public class UserNotFoundException : Exception
{
    public string Username { get; }
    
    public UserNotFoundException(string username)
        : base($"ユーザー '{username}' が見つかりません")
    {
        Username = username;
    }
}

// 使用例
if (user == null)
{
    throw new UserNotFoundException(username);
}
```

### 例外フィルタ

```csharp
try
{
    // コード
}
catch (Exception ex) when (ex.InnerException != null)
{
    // InnerExceptionがnullでない場合のみキャッチ
}
catch (IOException ex) when (ex.Message.Contains("disk"))
{
    // 特定のメッセージを含むIOExceptionをキャッチ
}
```

## 非同期プログラミング

### async/await

```csharp
// 非同期メソッド
public async Task<string> DownloadDataAsync(string url)
{
    HttpClient client = new HttpClient();
    string result = await client.GetStringAsync(url);
    return result;
}

// 非同期メソッドの呼び出し
public async Task ProcessDataAsync()
{
    string data = await DownloadDataAsync("https://example.com");
    Console.WriteLine(data);
}
```

### タスクの作成と操作

```csharp
// Task.Run でバックグラウンド処理
Task task = Task.Run(() => 
{
    // 長時間実行される処理
});

// 複数のタスクの待機
Task task1 = Task.Run(() => { /* 処理1 */ });
Task task2 = Task.Run(() => { /* 処理2 */ });
await Task.WhenAll(task1, task2);

// いずれかのタスク完了を待機
Task completedTask = await Task.WhenAny(task1, task2);

// キャンセレーショントークン
CancellationTokenSource cts = new CancellationTokenSource();
CancellationToken token = cts.Token;

Task cancelableTask = Task.Run(() => 
{
    for (int i = 0; i < 100; i++)
    {
        token.ThrowIfCancellationRequested();
        // 処理
    }
}, token);

// タスクのキャンセル
cts.Cancel();
```

### ValueTask

```csharp
// キャッシュからの結果取得など、割り当てを減らせる場合に有用
public ValueTask<int> GetValueAsync()
{
    if (_cache.TryGetValue("key", out int value))
    {
        return new ValueTask<int>(value);
    }
    
    return new ValueTask<int>(SlowFetchAsync());
}
```

### 非同期ストリーム (.NET Core 3.0以降)

```csharp
// IAsyncEnumerable を返す
public async IAsyncEnumerable<int> GenerateSequenceAsync()
{
    for (int i = 0; i < 10; i++)
    {
        await Task.Delay(100);  // 非同期操作
        yield return i;
    }
}

// await foreach で消費
await foreach (var number in GenerateSequenceAsync())
{
    Console.WriteLine(number);
}
```

## ファイル操作

### 同期ファイル操作

```csharp
// ファイル読み込み
string content = File.ReadAllText("file.txt");
string[] lines = File.ReadAllLines("file.txt");
byte[] bytes = File.ReadAllBytes("file.bin");

// ファイル書き込み
File.WriteAllText("output.txt", "内容");
File.WriteAllLines("lines.txt", new[] { "行1", "行2" });
File.WriteAllBytes("output.bin", byteArray);

// ファイル追加
File.AppendAllText("log.txt", "新しいログエントリ\n");

// ファイル・ディレクトリ存在確認
bool fileExists = File.Exists("file.txt");
bool dirExists = Directory.Exists("directory");

// ファイル・ディレクトリ操作
File.Copy("source.txt", "destination.txt", overwrite: true);
File.Move("old.txt", "new.txt");
File.Delete("delete.txt");

Directory.CreateDirectory("newdir");
Directory.Delete("olddir", recursive: true);
string[] files = Directory.GetFiles("dir", "*.txt");
```

### 非同期ファイル操作

```csharp
// 非同期ファイル読み込み
string content = await File.ReadAllTextAsync("file.txt");
string[] lines = await File.ReadAllLinesAsync("file.txt");
byte[] bytes = await File.ReadAllBytesAsync("file.bin");

// 非同期ファイル書き込み
await File.WriteAllTextAsync("output.txt", "内容");
await File.WriteAllLinesAsync("lines.txt", new[] { "行1", "行2" });
await File.WriteAllBytesAsync("output.bin", byteArray);

// ストリームを使用した非同期操作
using FileStream fs = new FileStream("file.txt", FileMode.Open);
byte[] buffer = new byte[1024];
int bytesRead = await fs.ReadAsync(buffer, 0, buffer.Length);
await fs.WriteAsync(buffer, 0, bytesRead);
```

### パス操作

```csharp
string path = @"C:\directory\file.txt";
string directory = Path.GetDirectoryName(path);  // C:\directory
string fileName = Path.GetFileName(path);        // file.txt
string fileNameWithoutExt = Path.GetFileNameWithoutExtension(path);  // file
string extension = Path.GetExtension(path);      // .txt
string combinedPath = Path.Combine("directory", "file.txt");
```

## 属性

### 組み込み属性

```csharp
[Obsolete("このメソッドは非推奨です。NewMethod()を使用してください。")]
public void OldMethod() { }

[Serializable]
public class User { }

[NonSerialized]
private string temporaryData;

[DllImport("user32.dll")]
public static extern int MessageBox(IntPtr hWnd, string text, string caption, uint type);

[DebuggerDisplay("Name = {Name}")]
public class Person { public string Name { get; set; } }
```

### カスタム属性

```csharp
// カスタム属性の定義
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, AllowMultiple = true)]
public class AuthorAttribute : Attribute
{
    public string Name { get; }
    public string Email { get; set; }
    
    public AuthorAttribute(string name)
    {
        Name = name;
    }
}

// カスタム属性の使用
[Author("John Doe", Email = "john@example.com")]
public class SampleClass { }

// リフレクションで属性を取得
Type type = typeof(SampleClass);
AuthorAttribute[] attributes = (AuthorAttribute[])type.GetCustomAttributes(typeof(AuthorAttribute), false);
```

## C# 8.0～12.0の主な新機能

### C# 8.0 (.NET Core 3.0+)

```csharp
// readonly メンバー
public readonly double GetArea() => Math.PI * Radius * Radius;

// デフォルトインターフェイス実装
interface ILogger
{
    void Log(string message);
    void LogError(string message) => Log($"ERROR: {message}");
}

// using宣言
using var file = new StreamReader("file.txt");
// スコープ終了時に自動的にDisposeされる

// switch式
string category = size switch
{
    <= 0 => "無効",
    < 10 => "小",
    < 100 => "中",
    _ => "大"
};

// null合体代入演算子
string name = null;
name ??= "デフォルト名";

// 静的ローカル関数
static int Add(int a, int b) => a + b;

// インデックスとレンジ
string text = "Hello, World!";
char last = text[^1];       // '!'（末尾から数えて1番目）
string sub = text[0..5];    // "Hello"（0から5未満まで）
string partial = text[..5]; // "Hello"（先頭から5未満まで）
string end = text[7..];     // "World!"（7から末尾まで）
string all = text[..];      // "Hello, World!"（全体）

// インデックス付き非同期ストリーム
await foreach (var item in GetItemsAsync().WithIndex())
{
    Console.WriteLine($"Index: {item.Index}, Value: {item.Value}");
}

// パターンマッチング拡張
if (obj is { } nonNull) // null以外の値のマッチング
```

// nullable参照型 #nullable enable string? nullableString = null; // OK string nonNullableString = null; // 警告 #nullable disable

### C# 9.0 (.NET 5+)

```csharp
// レコード型（イミュータブルな参照型）
public record Person(string FirstName, string LastName);

// レコードの使用
var person = new Person("John", "Doe");
var (firstName, lastName) = person; // 分解

// レコードの等価性比較と複製
var person2 = person with { LastName = "Smith" };
bool areEqual = person == new Person("John", "Doe"); // true

// init-only プロパティ
public class User
{
    public string Name { get; init; } // 初期化後に変更不可
}

// ターゲット型new式
List<int> numbers = new(); // List<int>型が推論される

// パターンマッチングの強化
bool IsLetter(char c) => c is >= 'a' and <= 'z' or >= 'A' and <= 'Z';

// トップレベルステートメント
// Program.csファイル内で直接記述可能（Main不要）
Console.WriteLine("Hello, World!");
```

### C# 10.0 (.NET 6+)

```csharp
// レコード構造体（値型のレコード）
public record struct Point(int X, int Y);

// 構造体の改善
public struct Size
{
    public int Width { get; init; } // initセッターが使用可能
    public int Height { get; init; }
}

// 暗黙的な using宣言（ファイル先頭記述不要）
// .csprojファイルで有効化:
// <ImplicitUsings>enable</ImplicitUsings>

// global using宣言（プロジェクト全体で有効）
// 別ファイルに記述:
// global using System.Collections.Generic;

// ファイルスコープの名前空間
namespace MyApp; // 以降のコードはすべてMyApp名前空間内

// 拡張プロパティパターン
if (customer is { Address: { City: "Tokyo" } })
{
    // Tokyoに住むカスタマー
}

// 定数文字列補間
const string prefix = "Hello";
const string message = $"{prefix}, World!"; // C# 10以降で可能

// 完全修飾のない名前空間
// file.cs
namespace MyApp;
// このファイル内のコードはすべてMyApp名前空間内
```

### C# 11.0 (.NET 7+)

```csharp
// 文字列リテラルの改善
string longText = """
    これは複数行の文字列リテラルです。
    インデントが自動的に処理されます。
    "引用符"も簡単に扱えます。
    """;

// UTF-8文字列リテラル
ReadOnlySpan<byte> utf8Str = "hello"u8;

// リストパターン
int[] numbers = [1, 2, 3, 4];
bool isStartWith12 = numbers is [1, 2, ..];

// パターンマッチでのリストパターン
if (numbers is [var first, var second, ..])
{
    Console.WriteLine($"First: {first}, Second: {second}");
}

// 必須メンバー
public class Person
{
    public required string Name { get; set; }
    public required int Age { get; set; }
}
// 必須メンバーはオブジェクト初期化時に設定する必要あり
var person = new Person { Name = "John", Age = 30 };

// 符号付きデータサイズのネイティブ整数型
nint nativeInt = 42;
nuint nativeUnsignedInt = 42;

// 静的抽象メンバー
public interface IAddable<T> where T : IAddable<T>
{
    static abstract T operator +(T a, T b);
}

// raw string literals
string json = """
    {
        "name": "John",
        "age": 30
    }
    """;
```

### C# 12.0 (.NET 8+)

```csharp
// 主要なコレクション式
int[] array = [1, 2, 3, 4, 5];
List<int> list = [1, 2, 3, 4, 5];
Dictionary<string, int> dict = ["one" => 1, "two" => 2];

// スプレッド演算子
int[] first = [1, 2, 3];
int[] second = [4, 5, 6];
int[] combined = [.. first, .. second]; // [1, 2, 3, 4, 5, 6]

// インラインの配列型
void Process([1, 2, 3]) { } // インラインの配列値

// default値をディスカード
public string Method(string a, string b = _) // _ はデフォルト値

// 型エイリアス
using Point = (int X, int Y);
Point p = (10, 20);

// プライマリコンストラクターの拡張
class Person(string name, int age) // プライマリコンストラクタ
{
    public string Name { get; } = name;
    public int Age { get; } = age;
    
    // コンストラクタボディはなし
}

// ref readonly パラメーター
void Process(ref readonly LargeStruct data)
{
    // dataを変更できないが、コピーを回避
}

// 実験的な属性
[Experimental("FEATURE01")]
public void ExperimentalMethod() { }

// interceptors（.NET 8のソースジェネレーター機能）
[InterceptsLocation("Program.cs", line: 10, character: 5)]
static void InterceptMethod() { }
```

## LINQ (言語統合クエリ)

### LINQ基本

```csharp
// LINQ to Objects
var numbers = new List<int> { 1, 2, 3, 4, 5 };

// メソッド構文
var evenNumbers = numbers.Where(n => n % 2 == 0);
var squares = numbers.Select(n => n * n);
var ordered = numbers.OrderByDescending(n => n);

// クエリ構文
var query = from n in numbers
            where n % 2 == 0
            orderby n
            select n * n;
```

### コレクション操作

```csharp
// フィルタリング
var filtered = numbers.Where(n => n > 3);
var taken = numbers.Take(3);
var skipped = numbers.Skip(2);
var distinct = numbers.Distinct();

// 射影
var doubled = numbers.Select(n => n * 2);
var anonymousType = numbers.Select(n => new { Value = n, Square = n * n });
var flat = nestedLists.SelectMany(list => list);

// 並べ替え
var ascending = numbers.OrderBy(n => n);
var descending = numbers.OrderByDescending(n => n);
var multiSort = people.OrderBy(p => p.LastName).ThenBy(p => p.FirstName);

// グループ化
var grouped = people.GroupBy(p => p.City);
foreach (var group in grouped)
{
    Console.WriteLine($"City: {group.Key}");
    foreach (var person in group)
    {
        Console.WriteLine($"  {person.Name}");
    }
}

// 結合
var joined = customers.Join(
    orders,
    customer => customer.Id,
    order => order.CustomerId,
    (customer, order) => new { customer.Name, order.Amount }
);

// グループ結合
var groupJoined = customers.GroupJoin(
    orders,
    customer => customer.Id,
    order => order.CustomerId,
    (customer, customerOrders) => new { 
        customer.Name, 
        Orders = customerOrders.ToList() 
    }
);
```

### 集計と要素操作

```csharp
// 集計
int count = numbers.Count();
int countFiltered = numbers.Count(n => n > 3);
int sum = numbers.Sum();
double average = numbers.Average();
int min = numbers.Min();
int max = numbers.Max();

// 要素取得
int first = numbers.First();
int firstOrDefault = numbers.FirstOrDefault();
int last = numbers.Last();
int lastOrDefault = numbers.LastOrDefault();
int single = numbers.Single(n => n == 3);
int singleOrDefault = numbers.SingleOrDefault(n => n == 3);
int elementAt = numbers.ElementAt(2);

// 条件チェック
bool any = numbers.Any(n => n > 10);
bool all = numbers.All(n => n > 0);
bool contains = numbers.Contains(5);
```

### 遅延評価とイミディエイト評価

```csharp
// 遅延評価 - 実際に列挙するまで実行されない
var query = numbers.Where(n => n > 3);

// イミディエイト評価 - すぐに実行される
var list = numbers.Where(n => n > 3).ToList();
var array = numbers.Where(n => n > 3).ToArray();
var dictionary = people.ToDictionary(p => p.Id);
var lookup = people.ToLookup(p => p.City);
```

### パイプラインとチェーン

```csharp
// 複数の操作をチェーン
var result = numbers
    .Where(n => n % 2 == 0)
    .Select(n => n * n)
    .OrderByDescending(n => n)
    .Take(3)
    .ToList();
```

## NuGet パッケージとプロジェクト管理

### パッケージ参照

```xml
<!-- .csproj ファイル内 -->
<ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="13.0.1" />
    <PackageReference Include="Microsoft.Extensions.DependencyInjection" Version="6.0.0" />
</ItemGroup>
```

### グローバルツール

```bash
# グローバルツールのインストール
dotnet tool install -g dotnet-ef

# グローバルツールの更新
dotnet tool update -g dotnet-ef

# グローバルツールの一覧
dotnet tool list -g
```

### プロジェクト設定

```xml
<!-- .csproj ファイル内 -->
<PropertyGroup>
    <TargetFramework>net8.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
    <LangVersion>12.0</LangVersion>
</PropertyGroup>
```

## 基本制御構造

### nullチェックパターン

```csharp
// null条件演算子とnull合体演算子
string name = person?.Name ?? "Unknown";

// nullチェックパターン
if (person is null)
{
    // personがnullの場合
}

if (person is not null)
{
    // personがnullでない場合
}

// nullチェック後のパターンマッチング
if (person is not null and { Age: > 18 })
{
    // personがnullでなく、18歳より上の場合
}
```

### エラー処理パターン

```csharp
// TryParseパターン
if (int.TryParse(input, out int result))
{
    // 変換成功、resultを使用
}
else
{
    // 変換失敗
}

// 例外処理と再スロー
try
{
    // コード
}
catch (Exception ex) when (ex is not CriticalException)
{
    // ログ記録
    Log(ex);
    throw;  // 元の例外を再スロー
}

// Result<T>パターン（戻り値でエラーを表現）
public Result<int> Divide(int a, int b)
{
    if (b == 0)
    {
        return Result<int>.Error("ゼロ除算");
    }
    return Result<int>.Success(a / b);
}
```

## 実用的なコードパターン

### ビルダーパターン

```csharp
var message = new MessageBuilder()
    .SetSender("system")
    .SetRecipient("user")
    .SetSubject("通知")
    .SetBody("これはテスト通知です。")
    .Build();
```

### ファクトリーパターン

```csharp
public abstract class Vehicle { }
public class Car : Vehicle { }
public class Truck : Vehicle { }

public static class VehicleFactory
{
    public static Vehicle Create(string type) => type.ToLower() switch
    {
        "car" => new Car(),
        "truck" => new Truck(),
        _ => throw new ArgumentException($"Unknown vehicle type: {type}")
    };
}
```

### シングルトンパターン

```csharp
public sealed class Singleton
{
    private static readonly Lazy<Singleton> _instance = 
        new Lazy<Singleton>(() => new Singleton());
        
    public static Singleton Instance => _instance.Value;
    
    private Singleton() { }
}
```

### 拡張メソッドの活用

```csharp
public static class StringExtensions
{
    public static bool IsValidEmail(this string email)
    {
        return !string.IsNullOrEmpty(email) &&
               email.Contains("@") &&
               email.Contains(".");
    }
}

// 使用例
bool isValid = "test@example.com".IsValidEmail();
```

### イベントとデリゲート

```csharp
// デリゲート定義
public delegate void MessageHandler(string message);

// イベント
public class MessageService
{
    public event MessageHandler? MessageReceived;
    
    public void ReceiveMessage(string message)
    {
        OnMessageReceived(message);
    }
    
    protected virtual void OnMessageReceived(string message)
    {
        MessageReceived?.Invoke(message);
    }
}

// イベント購読
var service = new MessageService();
service.MessageReceived += (message) => 
{
    Console.WriteLine($"受信: {message}");
};
```

## デバッグとテスト

### デバッグ用コード

```csharp
// コンディショナルコンパイル
#if DEBUG
Console.WriteLine("デバッグモードです");
#endif

// Debug静的クラス
Debug.WriteLine("デバッグ情報");
Debug.Assert(x > 0, "xは正の値である必要があります");

// デバッガーブレークポイント
if (errorCondition)
{
    Debugger.Break();  // デバッガー実行時にブレーク
}
```

### テストコード (MSTest)

```csharp
[TestClass]
public class CalculatorTests
{
    [TestMethod]
    public void Add_TwoNumbers_ReturnsSum()
    {
        // Arrange
        var calculator = new Calculator();
        
        // Act
        int result = calculator.Add(2, 3);
        
        // Assert
        Assert.AreEqual(5, result);
    }
    
    [TestMethod]
    [ExpectedException(typeof(DivideByZeroException))]
    public void Divide_ByZero_ThrowsException()
    {
        var calculator = new Calculator();
        calculator.Divide(10, 0);
    }
}
```

## 著作権表示

この C# 構文チートシートは個人的な学習および参照目的で作成されています。Microsoft、.NET、C#はMicrosoft Corporationの商標です。このドキュメントは公式ドキュメントではありません。正確な情報は常にMicrosoftの公式ドキュメントを参照してください。