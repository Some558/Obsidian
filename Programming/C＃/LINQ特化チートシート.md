# C# LINQ 詳細チートシート (.NET 8)

LINQ (Language Integrated Query) は、C#でコレクションデータに対するクエリ操作を統一的に行うための機能です。このチートシートでは、LINQの基本から応用までを詳細に解説します。

## 目次

1. [LINQ の基本](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#linq-%E3%81%AE%E5%9F%BA%E6%9C%AC)
2. [クエリ構文とメソッド構文](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E3%82%AF%E3%82%A8%E3%83%AA%E6%A7%8B%E6%96%87%E3%81%A8%E3%83%A1%E3%82%BD%E3%83%83%E3%83%89%E6%A7%8B%E6%96%87)
3. [フィルタリング操作](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E3%83%95%E3%82%A3%E3%83%AB%E3%82%BF%E3%83%AA%E3%83%B3%E3%82%B0%E6%93%8D%E4%BD%9C)
4. [並べ替え操作](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E4%B8%A6%E3%81%B9%E6%9B%BF%E3%81%88%E6%93%8D%E4%BD%9C)
5. [射影操作](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E5%B0%84%E5%BD%B1%E6%93%8D%E4%BD%9C)
6. [集計操作](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E9%9B%86%E8%A8%88%E6%93%8D%E4%BD%9C)
7. [要素操作](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E8%A6%81%E7%B4%A0%E6%93%8D%E4%BD%9C)
8. [集合操作](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E9%9B%86%E5%90%88%E6%93%8D%E4%BD%9C)
9. [結合操作](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E7%B5%90%E5%90%88%E6%93%8D%E4%BD%9C)
10. [グループ化操作](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E3%82%B0%E3%83%AB%E3%83%BC%E3%83%97%E5%8C%96%E6%93%8D%E4%BD%9C)
11. [パーティション操作](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E3%83%91%E3%83%BC%E3%83%86%E3%82%A3%E3%82%B7%E3%83%A7%E3%83%B3%E6%93%8D%E4%BD%9C)
12. [型変換操作](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E5%9E%8B%E5%A4%89%E6%8F%9B%E6%93%8D%E4%BD%9C)
13. [生成操作](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E7%94%9F%E6%88%90%E6%93%8D%E4%BD%9C)
14. [遅延評価と即時評価](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E9%81%85%E5%BB%B6%E8%A9%95%E4%BE%A1%E3%81%A8%E5%8D%B3%E6%99%82%E8%A9%95%E4%BE%A1)
15. [パフォーマンス最適化](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9%E6%9C%80%E9%81%A9%E5%8C%96)
16. [応用パターン](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E5%BF%9C%E7%94%A8%E3%83%91%E3%82%BF%E3%83%BC%E3%83%B3)
17. [LINQ to Entities (Entity Framework)](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#linq-to-entities-entity-framework)
18. [LINQ to XML](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#linq-to-xml)
19. [並列 LINQ (PLINQ)](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E4%B8%A6%E5%88%97-linq-plinq)
20. [.NET 6-8 の新機能](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#net-6-8-%E3%81%AE%E6%96%B0%E6%A9%9F%E8%83%BD)

## LINQ の基本

### 名前空間のインポート

```csharp
using System.Linq;  // LINQメソッドを使用するために必要
```

### データソース

LINQ は様々なデータソースに対して使用できます：

```csharp
// 配列
int[] numbers = { 1, 2, 3, 4, 5 };

// List
List<string> names = new List<string> { "Alice", "Bob", "Charlie" };

// Dictionary
Dictionary<string, int> ages = new Dictionary<string, int>
{
    ["Alice"] = 25,
    ["Bob"] = 30,
    ["Charlie"] = 35
};

// カスタムクラスのコレクション
List<Person> people = new List<Person>
{
    new Person { Id = 1, Name = "Alice", Age = 25, City = "New York" },
    new Person { Id = 2, Name = "Bob", Age = 30, City = "London" },
    new Person { Id = 3, Name = "Charlie", Age = 35, City = "Tokyo" }
};
```

## クエリ構文とメソッド構文

LINQ には 2 つの構文があります：

### クエリ構文

SQL に似た構文です：

```csharp
// クエリ構文
var results = from person in people
              where person.Age > 25
              orderby person.Name
              select new { person.Name, person.Age };
```

### メソッド構文

メソッドチェーンを使用する構文です：

```csharp
// メソッド構文
var results = people
    .Where(person => person.Age > 25)
    .OrderBy(person => person.Name)
    .Select(person => new { person.Name, person.Age });
```

### 変換対応表

|クエリ構文|メソッド構文|
|---|---|
|`from`|開始点|
|`where`|`Where()`|
|`orderby`|`OrderBy()`, `OrderByDescending()`|
|`select`|`Select()`|
|`group by`|`GroupBy()`|
|`join`|`Join()`|
|`let`|中間変数を伴う追加の `Select()`|
|`into`|継続変数|

## フィルタリング操作

### Where

条件に一致する要素をフィルタリングします：

```csharp
// 基本的なフィルタリング
var adults = people.Where(p => p.Age >= 18);

// 複数条件
var filteredPeople = people.Where(p => p.Age > 25 && p.City == "Tokyo");

// インデックスを使用したフィルタリング
var everySecondItem = numbers.Where((n, index) => index % 2 == 0);
```

### OfType

特定の型の要素だけをフィルタリングします：

```csharp
// object配列から特定の型だけを抽出
object[] mixed = { "string", 1, 2.0, true, "another string" };
var onlyStrings = mixed.OfType<string>();  // ["string", "another string"]
```

## 並べ替え操作

### OrderBy / OrderByDescending

単一フィールドで昇順・降順に並べ替えます：

```csharp
// 昇順
var orderedByAge = people.OrderBy(p => p.Age);

// 降順
var orderedByAgeDesc = people.OrderByDescending(p => p.Age);
```

### ThenBy / ThenByDescending

複数フィールドで並べ替えます：

```csharp
// 複数フィールドでの並べ替え
var orderedPeople = people
    .OrderBy(p => p.City)           // まず市で昇順
    .ThenByDescending(p => p.Age);  // 次に年齢で降順
```

### Reverse

シーケンスの順序を逆にします：

```csharp
var reversed = numbers.Reverse();  // [5, 4, 3, 2, 1]
```

### カスタム比較

`IComparer<T>` を実装したカスタム比較子を使用できます：

```csharp
public class PersonComparer : IComparer<Person>
{
    public int Compare(Person x, Person y)
    {
        // 名前の長さで比較
        return x.Name.Length.CompareTo(y.Name.Length);
    }
}

var orderedByNameLength = people.OrderBy(p => p, new PersonComparer());
```

## 射影操作

### Select

各要素を新しい形式に変換します：

```csharp
// プロパティの抽出
var names = people.Select(p => p.Name);  // ["Alice", "Bob", "Charlie"]

// 匿名型への射影
var nameAgePairs = people.Select(p => new { p.Name, p.Age });

// インデックスを使った射影
var numbered = people.Select((p, index) => $"{index + 1}. {p.Name}");
                     // ["1. Alice", "2. Bob", "3. Charlie"]

// 計算値の射影
var ageInMonths = people.Select(p => new { p.Name, AgeInMonths = p.Age * 12 });
```

### SelectMany

入れ子になったコレクションをフラット化します：

```csharp
// 入れ子リストのフラット化
List<List<int>> nestedLists = new List<List<int>>
{
    new List<int> { 1, 2 },
    new List<int> { 3, 4, 5 },
    new List<int> { 6 }
};

var flattened = nestedLists.SelectMany(list => list);  // [1, 2, 3, 4, 5, 6]

// 関連オブジェクトの展開
class Customer
{
    public string Name { get; set; }
    public List<Order> Orders { get; set; }
}

class Order
{
    public int OrderId { get; set; }
    public decimal Amount { get; set; }
}

List<Customer> customers = GetCustomers();
var allOrders = customers.SelectMany(c => c.Orders);

// SelectManyを使った結合と射影
var customerOrders = customers.SelectMany(
    customer => customer.Orders,
    (customer, order) => new { CustomerName = customer.Name, order.OrderId, order.Amount }
);
```

## 集計操作

### Count / LongCount

要素の数をカウントします：

```csharp
// 全要素数
int count = numbers.Count();

// 条件を満たす要素数
int evenCount = numbers.Count(n => n % 2 == 0);

// 大きなコレクション（int.MaxValueを超える場合）
long bigCount = hugeCollection.LongCount();
```

### Sum

数値の合計を計算します：

```csharp
// 単純な合計
int sum = numbers.Sum();  // 1 + 2 + 3 + 4 + 5 = 15

// プロパティの合計
int totalAge = people.Sum(p => p.Age);

// nullableプロパティの合計
decimal? totalAmount = orders.Sum(o => o.Amount);
```

### Average

平均値を計算します：

```csharp
// 単純な平均
double average = numbers.Average();  // (1 + 2 + 3 + 4 + 5) / 5 = 3

// プロパティの平均
double averageAge = people.Average(p => p.Age);
```

### Min / Max

最小値/最大値を取得します：

```csharp
// 最小値
int min = numbers.Min();  // 1

// 最大値
int max = numbers.Max();  // 5

// プロパティの最小値/最大値
int youngestAge = people.Min(p => p.Age);
int oldestAge = people.Max(p => p.Age);

// オブジェクト自体を取得
Person youngest = people.OrderBy(p => p.Age).First();
Person oldest = people.OrderBy(p => p.Age).Last();
```

### Aggregate

カスタム集計操作を実行します：

```csharp
// 積の計算
int product = numbers.Aggregate((a, b) => a * b);  // 1 * 2 * 3 * 4 * 5 = 120

// 初期値を使用
int sumPlusTen = numbers.Aggregate(10, (sum, n) => sum + n);  // 10 + 1 + 2 + 3 + 4 + 5 = 25

// 複雑な集計（平均と分散）
var stats = numbers.Aggregate(
    new { Count = 0, Sum = 0, SumOfSquares = 0 },
    (acc, n) => new {
        Count = acc.Count + 1,
        Sum = acc.Sum + n,
        SumOfSquares = acc.SumOfSquares + n * n
    },
    acc => new {
        Count = acc.Count,
        Average = (double)acc.Sum / acc.Count,
        Variance = (double)acc.SumOfSquares / acc.Count - Math.Pow((double)acc.Sum / acc.Count, 2)
    }
);
```

## 要素操作

### First / FirstOrDefault

最初の要素を取得します：

```csharp
// 最初の要素
int first = numbers.First();  // 1

// 条件を満たす最初の要素
Person adultPerson = people.First(p => p.Age >= 18);

// シーケンスが空または条件を満たす要素がない場合、デフォルト値を返す
int? firstEven = numbers.FirstOrDefault(n => n % 2 == 0);  // 2
int? firstOver100 = numbers.FirstOrDefault(n => n > 100);  // 0 (int型のデフォルト値)

// .NET 6以降：デフォルト値を指定
int firstOver100WithDefault = numbers.FirstOrDefault(n => n > 100, -1);  // -1
```

### Last / LastOrDefault

最後の要素を取得します：

```csharp
// 最後の要素
int last = numbers.Last();  // 5

// 条件を満たす最後の要素
int lastEven = numbers.Last(n => n % 2 == 0);  // 4

// シーケンスが空または条件を満たす要素がない場合、デフォルト値を返す
int? lastOver100 = numbers.LastOrDefault(n => n > 100);  // 0
```

### Single / SingleOrDefault

唯一の要素を取得します（複数ある場合は例外）：

```csharp
// 唯一の要素（要素が1つでない場合は例外）
int single = (new[] { 42 }).Single();  // 42

// 条件を満たす唯一の要素
Person person = people.Single(p => p.Id == 2);  // Bobのみ

// 要素がない場合はデフォルト値、複数ある場合は例外
Person nullPerson = people.SingleOrDefault(p => p.Id == 999);  // null
```

### ElementAt / ElementAtOrDefault

指定インデックスの要素を取得します：

```csharp
// 指定インデックスの要素
int third = numbers.ElementAt(2);  // 3（0から始まるインデックス）

// 範囲外のインデックスの場合はデフォルト値
int? outOfRange = numbers.ElementAtOrDefault(10);  // 0
```

### DefaultIfEmpty

空のシーケンスの場合にデフォルト値を提供します：

```csharp
// 空のシーケンスにデフォルト値を設定
var emptyList = new List<int>();
var withDefault = emptyList.DefaultIfEmpty();  // [0]
var withCustomDefault = emptyList.DefaultIfEmpty(10);  // [10]
```

## 集合操作

### Distinct

重複を除去します：

```csharp
// 重複を除去
int[] withDuplicates = { 1, 2, 3, 1, 2, 4, 5 };
var distinct = withDuplicates.Distinct();  // [1, 2, 3, 4, 5]

// カスタム等価比較子を使用
var distinctPeople = people.Distinct(new PersonEqualityComparer());

public class PersonEqualityComparer : IEqualityComparer<Person>
{
    public bool Equals(Person x, Person y)
    {
        return x.Name == y.Name && x.Age == y.Age;
    }

    public int GetHashCode(Person obj)
    {
        return obj.Name.GetHashCode() ^ obj.Age.GetHashCode();
    }
}
```

### Union

和集合を取得します（重複なし）：

```csharp
int[] set1 = { 1, 2, 3 };
int[] set2 = { 3, 4, 5 };
var union = set1.Union(set2);  // [1, 2, 3, 4, 5]
```

### Intersect

積集合を取得します：

```csharp
int[] set1 = { 1, 2, 3 };
int[] set2 = { 3, 4, 5 };
var intersection = set1.Intersect(set2);  // [3]
```

### Except

差集合を取得します：

```csharp
int[] set1 = { 1, 2, 3 };
int[] set2 = { 3, 4, 5 };
var difference = set1.Except(set2);  // [1, 2]
```

### DistinctBy / UnionBy / IntersectBy / ExceptBy （.NET 6以降）

特定のキーに基づいて集合操作を行います：

```csharp
// 名前に基づいて重複を除去
var distinctByName = people.DistinctBy(p => p.Name);

// 年齢に基づいて和集合
var unionByAge = people1.UnionBy(people2, p => p.Age);

// 市に基づいて積集合
var intersectByCity = people1.IntersectBy(people2.Select(p => p.City), p => p.City);

// 名前に基づいて差集合
var exceptByName = people1.ExceptBy(people2.Select(p => p.Name), p => p.Name);
```

## 結合操作

### Join

内部結合を行います：

```csharp
var customers = new List<Customer>
{
    new Customer { Id = 1, Name = "Alice" },
    new Customer { Id = 2, Name = "Bob" },
    new Customer { Id = 3, Name = "Charlie" }
};

var orders = new List<Order>
{
    new Order { Id = 101, CustomerId = 1, Amount = 100 },
    new Order { Id = 102, CustomerId = 1, Amount = 200 },
    new Order { Id = 103, CustomerId = 2, Amount = 300 },
    new Order { Id = 104, CustomerId = 4, Amount = 400 }  // 存在しない顧客ID
};

// 内部結合
var customerOrders = customers.Join(
    orders,
    customer => customer.Id,       // 外部シーケンスのキーセレクター
    order => order.CustomerId,     // 内部シーケンスのキーセレクター
    (customer, order) => new       // 結果セレクター
    {
        CustomerName = customer.Name,
        OrderId = order.Id,
        order.Amount
    }
);
// 結果: Alice/101/100, Alice/102/200, Bob/103/300
```

### GroupJoin

左外部結合に似た操作を行います：

```csharp
// グループ結合（左外部結合に似ている）
var customersWithOrders = customers.GroupJoin(
    orders,
    customer => customer.Id,
    order => order.CustomerId,
    (customer, customerOrders) => new
    {
        CustomerName = customer.Name,
        Orders = customerOrders.ToList(),
        TotalAmount = customerOrders.Sum(o => o.Amount)
    }
);
// 結果: Alice/[101,102]/300, Bob/[103]/300, Charlie/[]/0
```

### Zip

複数のシーケンスを結合します：

```csharp
int[] numbers = { 1, 2, 3 };
string[] words = { "one", "two", "three" };

// 2つのシーケンスを結合
var zipped = numbers.Zip(words, (n, w) => $"{n} is {w}");
// 結果: ["1 is one", "2 is two", "3 is three"]

// 3つのシーケンスを結合 (.NET 6以降)
char[] symbols = { 'A', 'B', 'C' };
var zipped3 = numbers.Zip(words, symbols);
// 結果: [(1, "one", 'A'), (2, "two", 'B'), (3, "three", 'C')]
```

## グループ化操作

### GroupBy

要素をグループ化します：

```csharp
// 単純なグループ化
var peopleByCity = people.GroupBy(p => p.City);

foreach (var cityGroup in peopleByCity)
{
    Console.WriteLine($"City: {cityGroup.Key}");
    foreach (var person in cityGroup)
    {
        Console.WriteLine($"  {person.Name}, {person.Age}");
    }
}

// 要素セレクターを使用したグループ化
var namesByCity = people.GroupBy(
    p => p.City,          // キーセレクター
    p => p.Name           // 要素セレクター
);

// 結果セレクターを使用したグループ化
var cityStats = people.GroupBy(
    p => p.City,          // キーセレクター
    (city, cityPeople) => new  // 結果セレクター
    {
        City = city,
        Count = cityPeople.Count(),
        AverageAge = cityPeople.Average(p => p.Age),
        Names = string.Join(", ", cityPeople.Select(p => p.Name))
    }
);

// 複合キーでのグループ化
var groupedByAgeBracketAndCity = people.GroupBy(
    p => new { AgeBracket = p.Age / 10 * 10, p.City }
);
```

### ToLookup

GroupByに似ていますが、すぐに評価され、結果はルックアップテーブルになります：

```csharp
// ルックアップテーブル作成
var peopleByCity = people.ToLookup(p => p.City);

// 特定のキーに対する要素を取得
var tokyoPeople = peopleByCity["Tokyo"];
var nyPeople = peopleByCity["New York"];

// 要素セレクターの使用
var namesByCity = people.ToLookup(
    p => p.City,          // キーセレクター
    p => p.Name           // 要素セレクター
);
```

## パーティション操作

### Take / TakeLast

指定した数の要素を先頭/末尾から取得します：

```csharp
// 先頭から3要素
var firstThree = numbers.Take(3);  // [1, 2, 3]

// 末尾から2要素 (.NET Core 2.0以降)
var lastTwo = numbers.TakeLast(2);  // [4, 5]

// 条件を満たす限り要素を取得 (.NET 6以降)
var takeWhileUnderFour = numbers.TakeWhile(n => n < 4);  // [1, 2, 3]
```

### Skip / SkipLast

指定した数の要素を先頭/末尾からスキップします：

```csharp
// 先頭から2要素をスキップ
var skipTwo = numbers.Skip(2);  // [3, 4, 5]

// 末尾から3要素をスキップ (.NET Core 2.0以降)
var skipLastThree = numbers.SkipLast(3);  // [1, 2]

// 条件を満たす限り要素をスキップ
var skipWhileUnderThree = numbers.SkipWhile(n => n < 3);  // [3, 4, 5]
```

### Chunk （.NET 6以降）

シーケンスを指定サイズのチャンクに分割します：

```csharp
// 2要素ずつのチャンクに分割
var chunks = Enumerable.Range(1, 7).Chunk(2);
// 結果: [[1,2], [3,4], [5,6], [7]]

// チャンクの処理
foreach (var chunk in chunks)
{
    Console.WriteLine($"Chunk: {string.Join(", ", chunk)}");
}
```

## 型変換操作

### ToArray / ToList / ToDictionary / ToHashSet

シーケンスを別のコレクション型に変換します：

```csharp
// 配列に変換
int[] array = numbers.ToArray();

// リストに変換
List<int> list = numbers.ToList();

// 辞書に変換
Dictionary<int, Person> personById = people.ToDictionary(
    p => p.Id    // キーセレクター
);

// 値セレクターを使用した辞書
Dictionary<string, int> ageByName = people.ToDictionary(
    p => p.Name,    // キーセレクター
    p => p.Age      // 値セレクター
);

// HashSetに変換 (.NET Core 2.0以降)
HashSet<int> set = numbers.ToHashSet();
```

### AsEnumerable / AsQueryable

シーケンスの型を変換します：

```csharp
// IEnumerable<T>に変換
IEnumerable<int> enumerable = numbers.AsEnumerable();

// IQueryable<T>に変換（LINQ to SQL/Entities等で使用）
IQueryable<Person> queryable = people.AsQueryable();
```

### Cast / OfType

要素の型を変換します：

```csharp
// すべての要素を指定した型にキャスト（互換性がない場合は例外）
ArrayList arrayList = new ArrayList { 1, 2, 3 };
IEnumerable<int> ints = arrayList.Cast<int>();

// 指定した型の要素だけをフィルタリング
ArrayList mixed = new ArrayList { 1, "two", 3, "four" };
IEnumerable<string> strings = mixed.OfType<string>();  // ["two", "four"]
```

## 生成操作

### Range

指定範囲の整数シーケンスを生成します：

```csharp
// 0から9までの整数を生成
var zeroToNine = Enumerable.Range(0, 10);

// 1から100までの奇数を生成
var oddNumbers = Enumerable.Range(1, 50).Select(n => n * 2 - 1);
```

### Repeat

指定した要素を繰り返すシーケンスを生成します：

```csharp
// 0を10回繰り返す
var zeros = Enumerable.Repeat(0, 10);

// オブジェクトを繰り返す
var defaultPersons = Enumerable.Repeat(new Person { Name = "Unknown" }, 5);
```

### Empty

空のシーケンスを生成します：

```csharp
var emptyCollection = Enumerable.Empty<int>();
```

## 遅延評価と即時評価

### 遅延評価

ほとんどのLINQ操作は遅延評価され、実際に要素にアクセスするまで実行されません：

```csharp
// これらの操作はまだ実行されていない
var query = numbers
    .Where(n => n % 2 == 0)
    .Select(n => n * n);

// 実際に列挙したときに初めて実行される
foreach (var item in query)
{
    Console.WriteLine(item);  // ここで初めてフィルタと射影が実行される
}
```

### 即時評価

一部の操作は即時に評価され、結果をメモリに格納します：

```csharp
// 即時評価される操作
int[] array = query.ToArray();       // 配列に変換（すぐに評価）
List<int> list = query.ToList();     // リストに変換（すぐに評価）
Dictionary<int, int> dict = query.ToDictionary(n => n, n => n * 10);
int count = query.Count();           // カウント
int sum = query.Sum();               // 合計
```

## パフォーマンス最適化

### パフォーマンスのベストプラクティス

```csharp
// 悪い例：複数回の列挙
var result1 = numbers.Where(n => n > 3);
Console.WriteLine($"Count: {result1.Count()}");
foreach (var item in result1) { Console.WriteLine(item); }

// 良い例：結果を保存して再利用
var result2 = numbers.Where(n => n > 3).ToList();  // すぐに評価して保存
Console.WriteLine($"Count: {result2.Count}");
foreach (var item in result2) { Console.WriteLine(item); }

// 悪い例：繰り返し使用する値を毎回計算
var items = Enumerable.Range(1, 1000);
var slowQuery = items.Where(i => Math.Sqrt(i) > 10);

// 良い例：計算結果をキャッシュ
var fastQuery = items.Select(i => new { Value = i, Sqrt = Math.Sqrt(i) })
                    .Where(x => x.Sqrt > 10)
                    .Select(x => x.Value);
```

### AsEnumerable vs AsQueryable

```csharp
// データベースクエリ最適化
using (var context = new MyDbContext())
{
    // 悪い例：すべてのユーザーをメモリに読み込んでからフィルタリング
    var users = context.Users.ToList();
    var activeUsers = users.Where(u => u.IsActive);

    // 良い例：データベースでフィルタリング
    var activeUsers2 = context.Users.Where(u => u.IsActive).ToList();
}
```

## 応用パターン

### パイプラインパターン

複数の操作を連鎖させて複雑な処理を行います：

```csharp
var result = sourceData
    .Where(item => item.IsValid)
    .GroupBy(item => item.Category)
    .Select(group => new CategorySummary
    {
        Category = group.Key,
        Count = group.Count(),
        Total = group.Sum(item => item.Value),
        Average = group.Average(item => item.Value),
        Min = group.Min(item => item.Value),
        Max = group.Max(item => item.Value)
    })
    .OrderByDescending(summary => summary.Total)
    .Take(5)
    .ToList();
```

### 複合フィルター

フィルター条件を動的に組み合わせます：

```csharp
IEnumerable<Person> FilterPeople(
    IEnumerable<Person> people,
    string nameFilter = null,
    int? minAge = null,
    int? maxAge = null,
    string cityFilter = null)
{
    // 条件を動的に適用
    if (!string.IsNullOrEmpty(nameFilter))
        query = query.Where(p => p.Name.Contains(nameFilter));
    
    if (minAge.HasValue)
        query = query.Where(p => p.Age >= minAge.Value);
    
    if (maxAge.HasValue)
        query = query.Where(p => p.Age <= maxAge.Value);
    
    if (!string.IsNullOrEmpty(cityFilter))
        query = query.Where(p => p.City == cityFilter);
    
    return query;
}
```

### レコードのマージと比較

異なるソースからのレコードを結合して比較します：

```csharp
// データソース1からのレコード
var records1 = GetSource1Records();

// データソース2からのレコード
var records2 = GetSource2Records();

// IDをキーにしてマージ
var merged = records1
    .Select(r1 => new { Record1 = r1, Id = r1.Id })
    .Join(
        records2.Select(r2 => new { Record2 = r2, Id = r2.Id }),
        r1 => r1.Id,
        r2 => r2.Id,
        (r1, r2) => new {
            Id = r1.Id,
            Record1 = r1.Record1,
            Record2 = r2.Record2,
            HasDifferences = r1.Record1.Amount != r2.Record2.Amount || 
                             r1.Record1.Date != r2.Record2.Date
        }
    )
    .ToList();

// 差異があるレコードを抽出
var differences = merged.Where(m => m.HasDifferences).ToList();
```

### フラットファイル処理

CSVや他のフラットファイルのデータ処理を行います：

```csharp
// CSVファイルを読み込んで処理
var lines = File.ReadAllLines("data.csv").Skip(1); // ヘッダーをスキップ

var parsedData = lines
    .Select(line => line.Split(','))
    .Where(parts => parts.Length == 4) // 有効な行のみ
    .Select(parts => new {
        Id = int.Parse(parts[0]),
        Name = parts[1],
        Value = decimal.Parse(parts[2]),
        Date = DateTime.Parse(parts[3])
    })
    .OrderBy(item => item.Date)
    .ToList();
```

## LINQ to Entities (Entity Framework)

### 基本的なクエリ

Entity Frameworkを使用したデータベースクエリを行います：

```csharp
using (var context = new MyDbContext())
{
    // 基本的なクエリ
    var activeUsers = context.Users
        .Where(u => u.IsActive)
        .OrderBy(u => u.LastName)
        .ToList();
    
    // 複雑なデータローディング（Include）
    var ordersWithCustomers = context.Orders
        .Include(o => o.Customer)
        .Include(o => o.OrderItems)
            .ThenInclude(i => i.Product)
        .Where(o => o.OrderDate > DateTime.Now.AddDays(-30))
        .ToList();
}
```

### データベース固有の関数

データベース固有の関数を使用します：

```csharp
using Microsoft.EntityFrameworkCore;

// SQLのLIKE演算子を使用
var searchResults = context.Products
    .Where(p => EF.Functions.Like(p.Name, "%keyword%"))
    .ToList();

// 日付関数
var thisYearOrders = context.Orders
    .Where(o => o.OrderDate.Year == DateTime.Now.Year)
    .ToList();

// グループ化と集計
var salesByCategory = context.OrderItems
    .GroupBy(i => i.Product.Category)
    .Select(g => new {
        Category = g.Key,
        TotalSales = g.Sum(i => i.Quantity * i.UnitPrice)
    })
    .OrderByDescending(x => x.TotalSales)
    .ToList();
```

### SQLを直接実行

生のSQLクエリを実行します：

```csharp
// Raw SQL実行
var results = context.Products
    .FromSqlRaw("SELECT * FROM Products WHERE Price > {0}", 100)
    .ToList();

// ストアドプロシージャ
var customers = context.Customers
    .FromSqlRaw("EXEC GetTopCustomers @p0", 10)
    .ToList();
```

## LINQ to XML

### XML文書の作成と操作

LINQ to XMLを使用してXML文書を操作します：

```csharp
using System.Xml.Linq;

// XML作成
XDocument doc = new XDocument(
    new XDeclaration("1.0", "utf-8", "yes"),
    new XElement("Root",
        new XElement("Customer",
            new XAttribute("Id", 1),
            new XElement("Name", "John Doe"),
            new XElement("Email", "john@example.com")
        ),
        new XElement("Customer",
            new XAttribute("Id", 2),
            new XElement("Name", "Jane Smith"),
            new XElement("Email", "jane@example.com")
        )
    )
);

// XML保存
doc.Save("customers.xml");

// XML読み込み
XDocument loadedDoc = XDocument.Load("customers.xml");

// XMLクエリ
var customers = loadedDoc.Descendants("Customer")
    .Select(c => new {
        Id = (int)c.Attribute("Id"),
        Name = (string)c.Element("Name"),
        Email = (string)c.Element("Email")
    })
    .ToList();

// XML変換
var updatedDoc = new XDocument(
    new XElement("Customers",
        from c in customers
        select new XElement("Customer",
            new XAttribute("Id", c.Id),
            new XElement("FullName", c.Name),
            new XElement("EmailAddress", c.Email)
        )
    )
);
```

### XPath と LINQ

XPathとLINQを組み合わせて使用します：

```csharp
using System.Xml.XPath;

// XPathを使ったXML要素の選択
var emailElements = doc.XPathSelectElements("//Customer/Email");
var customerNames = doc.XPathSelectElements("//Customer[Email='john@example.com']/Name")
    .Select(e => (string)e)
    .ToList();
```

## 並列 LINQ (PLINQ)

### 並列クエリ

複数のCPUコアを使用して並列処理を行います：

```csharp
// 基本的な並列クエリ
var parallelQuery = numbers.AsParallel().Where(n => IsExpensiveCheck(n));

// 順序の強制
var orderedQuery = numbers.AsParallel().AsOrdered()
    .Where(n => n % 2 == 0)
    .Select(n => n * n);

// 実行オプションの指定
var customParallelism = numbers.AsParallel()
    .WithDegreeOfParallelism(4)    // 使用するコア数を指定
    .WithExecutionMode(ParallelExecutionMode.ForceParallelism)
    .Where(n => IsExpensiveCheck(n));

// 並列クエリと例外処理
try
{
    var result = numbers.AsParallel()
        .Where(n => SomeMethodThatMightThrow(n))
        .ToList();
}
catch (AggregateException ex)
{
    // 複数の例外をまとめて処理
    foreach (var innerEx in ex.InnerExceptions)
    {
        Console.WriteLine($"Error: {innerEx.Message}");
    }
}
```

### ForAll による並列処理

並列にアクションを実行します：

```csharp
// 並列にアクションを実行
numbers.AsParallel().Where(n => n % 2 == 0).ForAll(n => {
    Console.WriteLine($"Processing {n} on thread {Thread.CurrentThread.ManagedThreadId}");
});
```

## .NET 6-8 の新機能

### .NET 6 の拡張機能

.NET 6でLINQに追加された新機能：

```csharp
// チャンク（要素を固定サイズのグループに分割）
IEnumerable<int[]> chunks = Enumerable.Range(1, 10).Chunk(3);
// [[1,2,3], [4,5,6], [7,8,9], [10]]

// 最大値と最小値をインデックス付きで取得
var source = new[] { 15, 1, 30, 4, 15 };
var minByIndex = source.MinBy(x => x);        // 1
var maxByIndex = source.MaxBy(x => x);        // 30

// ByとDistinctByでプロジェクション機能
var distinctCities = people.DistinctBy(p => p.City);
var unionCities = people1.UnionBy(people2, p => p.City);
var exceptCities = people1.ExceptBy(people2.Select(p => p.City), p => p.City);

// FirstOrDefault/LastOrDefaultのカスタムデフォルト値
int firstEven = numbers.FirstOrDefault(n => n > 100, -1);  // -1 (条件を満たす要素がない場合)

// ZipWithでタプルではなくカスタムオブジェクト
var zipped = Enumerable.Range(1, 3).Zip(new[] { "A", "B", "C" })
    .Select(tuple => new { Number = tuple.First, Letter = tuple.Second });
```

### .NET 7 の拡張機能

.NET 7で追加された新機能：

```csharp
// インデックス値とともに要素を取得
var items = new[] { "a", "b", "c" };
foreach (var (item, index) in items.Select((item, index) => (item, index)))
{
    Console.WriteLine($"{index}: {item}");
}

// Order/OrderDescending (キーセレクタなし)
var ordered = people.Order();  // IComparableの実装順
var descending = people.OrderDescending();
```

### .NET 8 の拡張機能

.NET 8で追加された新機能：

```csharp
// AggregateByでグループごとの集計
var customersByCity = customers.AggregateBy(
    keySelector: c => c.City,
    seed: new { Count = 0, TotalAge = 0 },
    func: (acc, c) => new { Count = acc.Count + 1, TotalAge = acc.TotalAge + c.Age }
);

// ElementAt/ElementAtOrDefaultの負のインデックス
var lastItem = array.ElementAt(^1);  // 配列の最後の要素
var secondToLast = array.ElementAt(^2);  // 後ろから2番目の要素

// Index/Rangeサポートの強化
var lastThree = array.Take(^3..);   // 後ろ3つの要素

// MaxByとMinByの改善
var oldestPerson = people.MaxBy(p => p.Age);  // 年齢が最大の人
var youngestPerson = people.MinBy(p => p.Age);  // 年齢が最小の人
```

## 高度な応用例

### 動的クエリビルダー

実行時に条件を動的に構築します：

```csharp
public static class QueryBuilder
{
    public static IQueryable<T> BuildQuery<T>(IQueryable<T> source, Dictionary<string, object> filters)
    {
        var parameter = Expression.Parameter(typeof(T), "x");
        Expression body = Expression.Constant(true);
        
        foreach (var filter in filters)
        {
            // プロパティアクセスの式を構築
            var property = Expression.Property(parameter, filter.Key);
            // 値との等価比較式を構築
            var value = Expression.Constant(filter.Value);
            var comparison = Expression.Equal(property, value);
            // ANDで既存の条件と結合
            body = Expression.AndAlso(body, comparison);
        }
        
        // ラムダ式を構築
        var lambda = Expression.Lambda<Func<T, bool>>(body, parameter);
        
        // Whereメソッドを適用
        return source.Where(lambda);
    }
}

// 使用例
var filters = new Dictionary<string, object>
{
    ["IsActive"] = true,
    ["City"] = "Tokyo"
};

var query = QueryBuilder.BuildQuery(context.Users, filters);
var result = query.ToList();
```

### カスタムLINQプロバイダ

独自のLINQプロバイダを実装して、カスタムデータソースへのLINQクエリをサポートします：

```csharp
// カスタムクエリプロバイダの実装例（簡略化）
public class CustomQueryProvider : IQueryProvider
{
    public IQueryable CreateQuery(Expression expression)
    {
        return new CustomQueryable(this, expression);
    }
    
    public IQueryable<TElement> CreateQuery<TElement>(Expression expression)
    {
        return new CustomQueryable<TElement>(this, expression);
    }
    
    public object Execute(Expression expression)
    {
        // 式ツリーを解析して実行
        return ExecuteExpression(expression);
    }
    
    public TResult Execute<TResult>(Expression expression)
    {
        return (TResult)Execute(expression);
    }
    
    private object ExecuteExpression(Expression expression)
    {
        // 式ツリーを解析してカスタムデータソースからデータを取得
        // 実際の実装はさらに複雑になる
        return null;
    }
}

// カスタムQueryableの実装
public class CustomQueryable<T> : IQueryable<T>
{
    private readonly Expression _expression;
    private readonly IQueryProvider _provider;
    
    public CustomQueryable(IQueryProvider provider, Expression expression)
    {
        _provider = provider;
        _expression = expression;
    }
    
    public Type ElementType => typeof(T);
    public Expression Expression => _expression;
    public IQueryProvider Provider => _provider;
    
    public IEnumerator<T> GetEnumerator()
    {
        return Provider.Execute<IEnumerable<T>>(Expression).GetEnumerator();
    }
    
    IEnumerator IEnumerable.GetEnumerator()
    {
        return GetEnumerator();
    }
}
```

### 複雑なクエリ最適化例

複雑なLINQクエリを最適化して、パフォーマンスを向上させます：

```csharp
// 最適化前
var result1 = products
    .Where(p => p.Category == "Electronics")
    .Select(p => new { p.Id, p.Name, p.Price })
    .Where(p => p.Price > 100)
    .OrderBy(p => p.Price)
    .Skip(10)
    .Take(10)
    .ToList();

// 最適化後（フィルターを先に実行して中間結果を減らす）
var result2 = products
    .Where(p => p.Category == "Electronics" && p.Price > 100)
    .OrderBy(p => p.Price)
    .Skip(10)
    .Take(10)
    .Select(p => new { p.Id, p.Name, p.Price })
    .ToList();
```

## LINQのベストプラクティス

### デバッグとエラー処理

```csharp
// クエリのデバッグ
var query = numbers.Where(n => n > 3);

// 中間結果を確認
var debug = query.ToList();  // ブレークポイントを設置

// 安全な要素アクセス
var first = query.FirstOrDefault() ?? 0;

// 例外処理
try
{
    var singleValue = query.Single();
}
catch (InvalidOperationException ex)
{
    Console.WriteLine("要素が見つからない、または複数存在します");
}
```

### パフォーマンス考慮事項

```csharp
// 悪い例：重複するフィルタリング
var filteredTwice = numbers
    .Where(n => n > 0)  // 最初のフィルター
    .Select(n => n * n)
    .Where(n => n > 10);  // 2回目のフィルター

// 良い例：一度のパスで完了
var filteredOnce = numbers
    .Where(n => {
        var isPositive = n > 0;
        var square = n * n;
        return isPositive && square > 10;
    });

// データベースクエリの最適化
// 悪い例：すべてのデータをメモリに読み込む
var allCustomers = context.Customers.ToList();
var filtered = allCustomers.Where(c => c.IsActive && c.Orders.Count > 0);

// 良い例：データベースでフィルタリング
var filteredCustomers = context.Customers
    .Where(c => c.IsActive)
    .Where(c => c.Orders.Count > 0)
    .ToList();
```

### 可読性とメンテナンス性

```csharp
// クエリロジックを分割する
var activeCustomers = customers.Where(c => c.IsActive);
var withRecentOrders = activeCustomers.Where(c => c.LastOrderDate > DateTime.Now.AddMonths(-3));
var topSpenders = withRecentOrders.OrderByDescending(c => c.TotalSpent).Take(10);

// ヘルパーメソッドで再利用可能な部分を抽出
IEnumerable<Customer> FilterActiveCustomers(IEnumerable<Customer> customers)
    => customers.Where(c => c.IsActive);

IEnumerable<Customer> FilterWithRecentOrders(IEnumerable<Customer> customers)
    => customers.Where(c => c.LastOrderDate > DateTime.Now.AddMonths(-3));

// より意図が明確になるコード
var topCustomers = customers
    .Where(c => c.IsActive)
    .Where(c => HasRecentActivity(c))
    .OrderByDescending(c => CalculateCustomerValue(c))
    .Take(10);
```

## 結論

このチートシートでは、LINQの基本から応用まで、C# (.NET 8)での実用的なLINQの使用方法を網羅しました。LINQはコレクションの操作とクエリを簡潔かつ表現力豊かに記述するための強力なツールです。適切に使用することで、コードの可読性、保守性、そしてパフォーマンスを向上させることができます。

このチートシートを参考に、日々のプログラミングでLINQを最大限に活用してください。