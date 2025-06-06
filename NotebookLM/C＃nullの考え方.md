提供されたソースに基づき、C#におけるnullとその取り扱い、および関連機能について網羅的に解説します。

nullとは

null は、多くのプログラミング言語、特にC#の参照型において、変数がいかなるオブジェクトも参照していない状態、すなわち無効な状態であることを示す特別な値です1...。このnull値に対してメンバーアクセスなどの操作を行おうとすると、System.NullReferenceException という実行時例外が発生します3。この例外はプログラミングにおける一般的なバグの原因の一つです4...。

nullの種類と基本的な扱い

C#には、nullを扱い得る変数には主に2つの種類があります。

1.

参照型: string やクラスのインスタンスなど、参照型の変数はデフォルトでnullになる可能性があります1...。

2.

値型: int や bool などの値型変数は、通常nullを取ることはできません1...。値型でnullを扱いたい場合は、null許容値型 (Nullable<T>構造体、またはシンタックスシュガーとして T? ) を使用します1...。

◦

null許容値型は、HasValue プロパティで値を持っているか判定し、Value プロパティで値を取得します（nullの場合はInvalidOperationExceptionをスロー）3。

◦

Nullable<T>.GetValueOrDefault() メソッドを使用すると、nullの場合は基になる値型のデフォルト値を取得できます5...。

nullを扱うための便利な演算子

C#には、nullをより簡潔に扱うためのいくつかの演算子があります。

•

null合体演算子 (??): 左側のオペランドがnullでない場合はその値を返します5...。nullの場合は右側のオペランドを評価し、その結果を返します8...。左側のオペランドがnullでない場合、右側のオペランドは評価されません（短絡評価）8...。null許容値型に対して、nullの場合に代替値を指定するのに役立ちます5...。右側のオペランドに throw 式を使用することで、引数チェックコードを簡潔に記述できます7...。

•

null結合代入演算子 (??=): 左側のオペランドがnullと評価された場合に限り、右側のオペランドの値を左側のオペランドに代入します8。左側のオペランドがnullでない場合、右側のオペランドは評価されません（短絡評価）8。これは、特定のコードフォームを置き換えるのに使用できます7。

•

null条件演算子 (?.): メンバーアクセス (.) 、インデクサーアクセス、またはデリゲート呼び出しを行う際に使用します9...。オペランド（左側）がnullでない場合は通常のアクセスを行います11。オペランドがnullの場合は、nullを返します（例外は発生しません）11...。これにより、明示的なnullチェックを記述せずにnullアクセスを回避できます11...。ただし、これはnull安全な型システムとは直接関係なく、null安全な言語を「使いやすくするための道具の1つ」です13...。

C# 8.0 以降の Null 許容参照型 (Nullable Reference Types: NRT)

C# 8.0 から導入されたNull許容参照型 (Nullable Reference Types) は、System.NullReferenceException の可能性を最小限に抑えるための一連の機能です1...。これは、参照型変数がnullを許容するかどうかをコードで明示的に宣言し、コンパイラがそれを静的に分析できるようにするものです15。

NRTの主要な機能は以下の通りです15...。

•

変数の注釈: 参照型変数の宣言時に ? をサフィックスとして付けることで、その変数がnullを許容する null許容参照型 であることを示します19...。? が付かない参照型変数は、デフォルトでnullを許容しない null非許容参照型 とみなされます（ただし、この挙動はNull許容コンテキスト設定に依存します）20...。null非許容参照型は、null以外の値で初期化される必要があり、null値を割り当てることはできません23。null許容参照型はnull値を割り当てることができます20。

•

コンパイラの静的分析 (null状態分析): コンパイラはコード中のすべての式の「null状態」をコンパイル時に追跡します17。null状態は not-null (nullでないことが確実) か maybe-null (nullになる可能性がある) のいずれかです17。コンパイラは、maybe-null と判断された変数を逆参照しようとすると警告を発します17。

•

APIシグネチャの属性: null状態分析の精度を向上させるため、API（メソッドの引数や戻り値など）に属性を付与して、そのnullセマンティクス（特定の条件で引数がnullでない、戻り値がnullでないなど）をコンパイラに伝えます18...。.NET 5 以降、すべての .NET ランタイム API に注釈が付けられています25。

•

コンパイラの警告: Null許容参照型が有効な場合、コンパイラはnullに関するさまざまな警告を発行し、ランタイムでの NullReferenceException 発生を防ぐ手助けをします26...。これには、null非許容型へのnullの代入の可能性 (CS8600, CS8601, CS8603, CS8604, CS8625など)26... や、nullの可能性がある値の逆参照 (CS8602, CS8605など)26... に関する警告が含まれます。その他、NULL値の許容の宣言の不一致に関する警告も多数存在します (CS8608 ～ CS8624, CS8631, CS8633, CS8634, CS8643, CS8644, CS8645, CS8667, CS8714, CS8764 ～ CS8769, CS8819)26...。また、コードが属性宣言の約束事に一致しない場合の警告 (CS8607, CS8763, CS8770, CS8774 ～ CS8777, CS8824, CS8825)26... や、switch式が一部のnull入力を処理しない場合の警告 (CS8655, CS8847) もあります26。

◦

これらの警告の一般的な対処法は、「必要なnullチェックの追加」、「? または ! Null許容注釈の追加」、「nullセマンティクスを記述する属性の追加」、「変数を正しく初期化する」のいずれかです27。

•

null免除演算子 (!): 開発者が変数は実際にはnullではないと分かっているものの、コンパイラの静的分析が maybe-null と判断してしまうような場合に、変数名の後に ! を付けることでコンパイラの分析をオーバーライドし、強制的に not-null 状態とみなさせることができます22...。これは警告を抑制しますが、実際のランタイムエラーを隠蔽する可能性もあります33。

•

Null許容コンテキスト: NRTの機能（警告と注釈）をプロジェクト全体または特定のファイルやコードブロックで有効/無効にする設定です18...。これは、プロジェクトファイルの <Nullable> 要素 (enable, disable, warnings, annotations)21... または #nullable プリプロセッサディレクティブ (enable, disable, restore) を使用して制御します35...。

◦

.NET 6 以降、新しいプロジェクトではデフォルトで <Nullable>enable</Nullable> が含まれます34...。既存プロジェクトのデフォルトは disabled です22...。

◦

Visual Studioのプロジェクトプロパティ「ビルド」タブで設定することも可能です35...。

◦

生成されたコードファイル (<auto-generated>, ファイル名パターンなど) には、グローバルなNull許容コンテキストは適用されず、デフォルトで disabled になります41。ジェネレーターは #nullable ディレクティブを使用してオプトインできます39。

•

ジェネリック: ジェネリック型引数についてもnullの許容性を制御できます18。型引数 T が参照型の場合、 T? はnull許容参照型を参照します。型引数 T が値型の場合、 T? は同じ値型 T を参照します42。class? や notnull といった新しい制約を使用して、型パラメーターがnull非許容参照型、null許容参照型、null非許容値型のどれであるべきかを指定できます43。

•

Null許容参照型とNull許容値型の実装の違い: Null許容値型は System.Nullable<T> 構造体として実装されますが、Null許容参照型はコンパイラによって読み取られる属性によって実装されます32...。例えば string? と string は同じ System.String 型ですが、 int? は System.Nullable<System.Int32>、 int は System.Int32 です32。

•

ライブラリ作成者への注意: Null許容参照型はコンパイル時機能であり、呼び出し元は警告を無視してnullを渡す可能性があります44。ライブラリ作成者は、null引数値に対する実行時チェックを含める必要があります44。ArgumentNullException.ThrowIfNull オプションの使用が推奨されています44。

•

既知の落とし穴: 配列や構造体に含まれる参照型については、静的分析が完全ではなく、警告なしにnull非許容参照がnullに初期化されてしまう可能性があるなど、注意が必要なケースが存在します18...。構造体では、コンストラクターが正常完了しても、静的分析がランタイム例外の有無を判断できない場合があるため警告が出ないことがあります45。

nullの判定・回避方法のまとめ

C#では、nullに関連する問題を回避するために、いくつかの方法が考えられます。

•

if文によるnullチェック: 最も基本的な方法です2...。if (obj != null) のように記述します2...。ただし、コード行数が増える傾向があります12。

•

null条件演算子 (?.) の使用: nullの可能性があるオブジェクトのメンバーにアクセスする際に使用し、NullReferenceException を回避します5...。

•

null合体演算子 (??) の使用: nullの可能性がある値に対して、nullだった場合の代替値を指定できます5。

•

Nullable<T>.GetValueOrDefault(): null許容値型がnullの場合に、基になる値型のデフォルト値を取得できます5...。

•

ArgumentNullException.ThrowIfNull: メソッドの引数がnullでないことを保証したい場合に、nullであれば ArgumentNullException をスローします44。

•

戻り値やコレクションにnullを使わない: メソッドが返す可能性のあるnullを避け、代わりに空のコレクションやデフォルト値を返すように設計することで、呼び出し側でのnullチェックの必要性を減らせます47。

•

Null許容参照型を有効にする: プロジェクト設定でNRTを有効にすることで、コンパイラが潜在的なnull参照の問題を警告として検出し、開発者が実行前に修正できるように促します4...。これは「どうしたらうまく Null チェックできるのか？」から「どうしたらうまく Null チェック(しないといけない状況)を回避できるのか？」という考え方の転換につながります48。

null安全に関する考察

null安全とは、「nullになりえない型 T と nullになりうる型 T? を区別する型システム」を指します4...。これにより、「必要なnullチェックがコンパイラによって機械的に強制されるからnull安全になる」という考え方です13。Null Reference Exceptionが発生しうるコードをコンパイル時にエラーにしてくれる仕組みとも説明されます4。近年、KotlinやSwiftなど、C#以外の新しい言語でもnull安全が採用されています4。

Javaなどで広く採用された「参照型変数がデフォルトでnullを許容できる設計」は、「T型の変数にnullが代入できるという言語設計」という間違いだったという意見があります49。これは、メモリ上の表現の容易さ（無効な参照を数値0で表すなど）から、無効な参照をT型の参照それ自体で表すという機能の詰め込みすぎに起因すると考えられています50。常に有効な参照の型を持つC++の参照型と比較されることもあります51。

null安全な型システムのメリットは、nullに関するバグをコンパイル時に発見できること4...、人間による見落としがなくなること52...、nullに関するテストコードの記述を一部省略できること54 などが挙げられます。これにより、開発効率やソフトウェアの品質向上に貢献します55...。コンパイル待ち時間が増える可能性はありますが、開発スタイルを変えることで対応可能であり、型の正しさがコンパイラによって保証される利点があります57...。

ただし、新しい機能であるため、理解不足による誤用パターン（例えば ! や ?. を安易に多用したり33...、?? 0 や ?? "" を安易に使ったりする54 など）により、かえって問題を引き起こす可能性も指摘されています33。しかし、適切に学習して使用すれば、これらの問題は回避可能であり、全体としては生産性向上に寄与するという見方が示されています33。

また、Null Object Patternによるnull対策も存在します52。これは、nullの代わりに特殊な「NullObject」インスタンスを使用して、nullチェックによる分岐を減らす手法です60。しかし、文脈によっては結局分岐が必要になる場合があり、コードの見通しが悪化する可能性も指摘されています61。JSONデコードのような特定の文脈では有効な場合もありますが、null安全な型システムでも同様に簡潔に記述可能です62。タチの悪い「自称null」を作ることは、予期しない挙動を引き起こす可能性があるため避けるべきです63...。

C#のNull許容参照型は、このようなnull安全の思想を取り入れた機能であり、現代的なC#開発においてnullに関連するバグを減らすための重要な手段となります55。しかし、その効果を最大限に引き出すためには、機能の適切な理解と使用が必要です33。

---
提供されたソースに基づき、ASP.NET CoreのRazor Pagesにおけるnullの扱い方に関するベストプラクティスをまとめます。

Razor Pagesは、ページ中心のシナリオを効率的にコーディングできるように設計されており、`@page` ディレクティブによってコントローラーを介さずに直接リクエストを処理します。`PageModel` クラス（`.cshtml.cs` ファイル）には、リクエストを処理するためのハンドラーメソッド（例: `OnGet`, `OnPost`）が含まれ、これらのメソッドはモデルバインディングや検証機能と連携して動作します。nullを適切に扱うことは、堅牢なアプリケーション開発において重要です。

**1. Nullable Reference Types (NRT) の活用** C# 8以降で導入されたNullable Reference Types (NRT) を活用することで、コンパイル時にnullの可能性についてコンパイラの警告を得ることができ、コードのnull安全性を高めることができます。プロジェクトファイル (`.csproj`) に `<Nullable>enable</Nullable>` を追加することで、NRTを有効にできます。 NRTを有効にすると、参照型変数に `?` を付けない場合はnon-nullableとして扱われ、`?` を付けることでnullを許容するnullable reference typeとして宣言できます。これにより、設計意図としてnullを許容するか否かをコード上で明確に示せるようになります。`!` 演算子を使用すると、nullableな式がnullでないことをコンパイラに伝えることができます。

**2. システムの境界におけるnullチェック** ユーザー入力、サードパーティライブラリからの応答、標準ライブラリの戻り値など、**制御できないシステムの境界**から値を受け取る場合は、nullの可能性を考慮し、**適切にnullチェックを行う必要**があります。これらの境界からの入力は、予期しない値（nullを含む）を含む可能性があるためです。特に、システムの外部から消費するものを扱う場所ではnullチェックを行い、**null値をその関数スコープ外に漏らさない**ようにすることが推奨されています。

**3. コード内部における過剰なnullチェックを避ける** システムの内部で生成または管理され、コード設計によってnullにならないことが保証されている値に対して、すべての参照アクセスで**過剰なnullチェックを行うべきではありません**。これは冗長であり、コードを読みにくくするだけでなく、本来検出されるべき**プログラマーのエラーを隠蔽してしまう**可能性があります。もし内部でnullが発生する場合は、それはコードの設計やロジックにおける問題である可能性が高いため、チェックで隠すのではなく、その根本原因を修正するべきです。

**4. NullReferenceException (NRE) の考え方** NullReferenceException (NRE) は、しばしば**コードにおけるひどいバグ**であると見なされます。エラーを許容しすぎてシステムがエラーを隠蔽するのではなく、プロダクション環境ではNREが**ハードクラッシュにつながる**ように設計し、クラッシュダンプを作成して事後分析（ポストモーテムインスペクション）を容易にするという考え方もあります。これは、問題の発生箇所を早期に特定し、デバッグを促進するための一つのアプローチです。

**5. モデルバインディングと検証におけるnull** Razor PagesのPageModelでは、HTTPリクエストからデータがモデルにバインドされます。デフォルトでは、モデルプロパティの値が見つからなかった場合でも、モデル状態エラーは発生せず、Nullableなシンプル型は `null` に設定され、non-nullableな値型はデフォルト値（例: `int` は0）に設定されます。 ユーザー入力の検証を行う際には `ModelState.IsValid` をチェックします。サーバーサイドでは、`[Required]` 属性はnon-nullableなフィールドに対しては機能しませんが、モデルバインディングの失敗によるエラーが発生する可能性があります。non-nullableな型の必須フィールドに対してカスタムエラーメッセージを表示したい場合は、フィールドをNullableにするか、モデルバインディングのデフォルトエラーメッセージ (`The value '' is invalid` など) を `MvcOptions.ModelBindingMessageProvider.SetValueMustNotBeNullAccessor` で設定することでカスタマイズできます。

**6. エラーハンドリングミドルウェアの利用** ASP.NET Coreでは、エラーハンドリングのためにミドルウェアが提供されています。

- **開発環境**では、詳細なエラー情報を表示する**Developer Exception Page** (`UseDeveloperExceptionPage`) を使用します。
- **非開発環境**（プロダクションなど）では、ユーザーに詳細なエラー情報を表示しないように、カスタムエラーページへのリダイレクトやカスタムレスポンスを生成する**Exception Handling Middleware** (`UseExceptionHandler`) を使用します。**敏感なエラー情報をクライアントに提供してはなりません**。
- 特定のHTTPステータスコード（例: 404 Not Found）に対してデフォルトのテキストレスポンスを有効にする `UseStatusCodePages` もありますが、これはプロダクション環境ではユーザーにとって有用でないため一般的ではありません。`UseStatusCodePages` は**例外をキャッチしない**ため、例外ハンドラーとは異なる役割を持ちます。
- エラーハンドリングを行うページ自体のコードも例外をスローする可能性があるため、プロダクション環境のエラーページは可能な限り静的なコンテンツで構成することが推奨されます。

**7. 設計によるnullの排除** 「Parse, don't validate」（検証するな、パースせよ）という考え方や、特定の抽象化においてnullを許容しないポリシーを持つことなど、**コード設計によってnullの発生自体を最小限に抑える**ことも重要なベストプラクティスです。パースが成功したオブジェクトは、無効な状態にならないことが理想です。Rustのようにnullがない言語でも、値が存在しない場合の処理は必要になります。これは、言語の機能だけでなく、コーディングの設計に tied したものです。

結論として、Razor Pagesにおけるnullの扱いのベストプラクティスは、C#のNRTを有効にしてコンパイラの助けを得つつ、外部からの入力など制御不能な境界では慎重にnullを扱い、コード内部では過剰なチェックを避けつつ設計でnullを排除・最小化し、意図しないNullReferenceExceptionは適切にエラーとして処理・報告する（隠蔽しない）、そしてASP.NET Coreのエラーハンドリングミドルウェアで環境に応じたエラー表示を適切に設定すること と言えます。