
# JavaScript 詳細チートシート (ES2022+)

## 目次

1. [基本構文](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E5%9F%BA%E6%9C%AC%E6%A7%8B%E6%96%87)
2. [変数と定数](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E5%A4%89%E6%95%B0%E3%81%A8%E5%AE%9A%E6%95%B0)
3. [データ型](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E3%83%87%E3%83%BC%E3%82%BF%E5%9E%8B)
4. [演算子](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E6%BC%94%E7%AE%97%E5%AD%90)
5. [制御構造](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E5%88%B6%E5%BE%A1%E6%A7%8B%E9%80%A0)
6. [関数](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E9%96%A2%E6%95%B0)
7. [オブジェクト](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)
8. [配列](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E9%85%8D%E5%88%97)
9. [文字列操作](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E6%96%87%E5%AD%97%E5%88%97%E6%93%8D%E4%BD%9C)
10. [日付と時間](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E6%97%A5%E4%BB%98%E3%81%A8%E6%99%82%E9%96%93)
11. [正規表現](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E6%AD%A3%E8%A6%8F%E8%A1%A8%E7%8F%BE)
12. [エラー処理](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E3%82%A8%E3%83%A9%E3%83%BC%E5%87%A6%E7%90%86)
13. [非同期処理](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E9%9D%9E%E5%90%8C%E6%9C%9F%E5%87%A6%E7%90%86)
14. [モジュール](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB)
15. [DOM操作](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#dom%E6%93%8D%E4%BD%9C)
16. [イベント処理](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E3%82%A4%E3%83%99%E3%83%B3%E3%83%88%E5%87%A6%E7%90%86)
17. [Fetch APIとAjax](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#fetch-api%E3%81%A8ajax)
18. [ローカルストレージ](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E3%83%AD%E3%83%BC%E3%82%AB%E3%83%AB%E3%82%B9%E3%83%88%E3%83%AC%E3%83%BC%E3%82%B8)
19. [クラス](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E3%82%AF%E3%83%A9%E3%82%B9)
20. [イテレータとジェネレータ](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E3%82%A4%E3%83%86%E3%83%AC%E3%83%BC%E3%82%BF%E3%81%A8%E3%82%B8%E3%82%A7%E3%83%8D%E3%83%AC%E3%83%BC%E3%82%BF)
21. [高階関数](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E9%AB%98%E9%9A%8E%E9%96%A2%E6%95%B0)
22. [デストラクチャリング](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E3%83%87%E3%82%B9%E3%83%88%E3%83%A9%E3%82%AF%E3%83%81%E3%83%A3%E3%83%AA%E3%83%B3%E3%82%B0)
23. [スプレッド構文とレスト構文](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E3%82%B9%E3%83%97%E3%83%AC%E3%83%83%E3%83%89%E6%A7%8B%E6%96%87%E3%81%A8%E3%83%AC%E3%82%B9%E3%83%88%E6%A7%8B%E6%96%87)
24. [プロキシとリフレクション](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E3%83%97%E3%83%AD%E3%82%AD%E3%82%B7%E3%81%A8%E3%83%AA%E3%83%95%E3%83%AC%E3%82%AF%E3%82%B7%E3%83%A7%E3%83%B3)
25. [Web API](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#web-api)
26. [ES2022以降の新機能](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#es2022%E4%BB%A5%E9%99%8D%E3%81%AE%E6%96%B0%E6%A9%9F%E8%83%BD)
27. [デバッグとパフォーマンス](https://claude.ai/chat/1101a936-2636-48c3-a269-bf06b4106370#%E3%83%87%E3%83%90%E3%83%83%E3%82%B0%E3%81%A8%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9)

## 基本構文

### コメント

```javascript
// 一行コメント

/* 複数行
   コメント */

/** JSDoc形式のドキュメントコメント
 * @param {string} name - 名前のパラメータ
 * @return {string} 挨拶メッセージ
 */
```

### セミコロン

```javascript
// 文の終了にセミコロンを使用（推奨）
let x = 5;
console.log(x);

// 自動セミコロン挿入（ASI）に注意
// 以下は関数の返り値ではなく undefined になる
function bad() {
  return
    { value: 42 }  // ASIによりreturnの後にセミコロンが挿入される
}

// 正しい書き方
function good() {
  return { 
    value: 42 
  };
}
```

### 大文字と小文字の区別

```javascript
let name = "value";
let Name = "Value";  // nameとNameは異なる変数
```

## 変数と定数

### 変数宣言

```javascript
// var - 関数スコープ（非推奨）
var oldVariable = "古い書き方";

// let - ブロックスコープ（推奨）
let modernVariable = "モダンな書き方";

// const - 再代入不可の定数（推奨）
const PI = 3.14159;
```

### スコープ

```javascript
// グローバルスコープ
let globalVar = "グローバル";

function testScope() {
  // 関数スコープ
  let functionVar = "関数内";
  
  if (true) {
    // ブロックスコープ
    let blockVar = "ブロック内";
    var leakyVar = "varは漏れる";
    
    console.log(globalVar);    // "グローバル"
    console.log(functionVar);  // "関数内"
    console.log(blockVar);     // "ブロック内"
  }
  
  console.log(leakyVar);       // "varは漏れる"
  // console.log(blockVar);    // エラー: blockVarはここでは見えない
}
```

### 変数巻き上げ (Hoisting)

```javascript
// 変数の巻き上げ
console.log(hoistedVar);  // undefined（エラーにならない）
var hoistedVar = "値";

// letとconstは巻き上げられるが、初期化されない（TDZ）
// console.log(hoistedLet);  // ReferenceError
let hoistedLet = "値";
```

## データ型

### プリミティブ型

```javascript
// 数値型（64ビット浮動小数点）
let integer = 42;
let float = 3.14;
let exponential = 2.998e8;
let binary = 0b1010;  // 10進数の10
let octal = 0o744;    // 10進数の484
let hex = 0xFF;       // 10進数の255
let bigInt = 9007199254740991n;  // BigInt型（整数の桁数制限なし）

// 文字列型
let single = 'シングルクォート';
let double = "ダブルクォート";
let template = `値: ${integer}`;  // テンプレートリテラル

// 論理型
let truthy = true;
let falsy = false;

// undefined型
let undef = undefined;

// null型
let empty = null;

// シンボル型（ES6）
let uniqueSymbol = Symbol('description');
let sharedSymbol = Symbol.for('shared');  // グローバルシンボルレジストリから取得

// BigInt型（ES2020）
let largePrimitive = 1234567890123456789012345678901234567890n;
```

### オブジェクト型

```javascript
// オブジェクトリテラル
let person = {
  name: "田中",
  age: 30,
  greet: function() {
    return `こんにちは、${this.name}さん`;
  }
};

// 配列
let array = [1, 2, 3, "文字列も可", { key: "値" }];

// 関数
function add(a, b) {
  return a + b;
}

// Date
let now = new Date();

// RegExp
let pattern = /\d+/g;
```

### 型変換

```javascript
// 明示的な変換
let num = Number("42");        // 文字列 -> 数値
let str = String(42);          // 数値 -> 文字列
let bool = Boolean(1);         // 数値 -> 論理値

// 暗黙的な変換
let result = "4" + 2;          // "42" (文字列連結)
let numericOperation = "4" - 2; // 2 (数値演算)
let condition = "非空文字列";  // true として評価される
if (condition) {
  // 実行される
}
```

### typeof演算子

```javascript
typeof 42;              // "number"
typeof "text";          // "string"
typeof true;            // "boolean"
typeof undefined;       // "undefined"
typeof null;            // "object" (JavaScript言語の仕様バグ)
typeof {};              // "object"
typeof [];              // "object"
typeof function() {};   // "function"
typeof Symbol();        // "symbol"
typeof 42n;             // "bigint"
```

## 演算子

### 算術演算子

```javascript
let a = 10, b = 3;

let sum = a + b;          // 13（加算）
let difference = a - b;   // 7（減算）
let product = a * b;      // 30（乗算）
let quotient = a / b;     // 3.3333...（除算）
let remainder = a % b;    // 1（剰余）
let power = a ** b;       // 1000（べき乗、ES2016）

// インクリメント・デクリメント
let c = 5;
c++;  // c = 6（後置インクリメント）
++c;  // c = 7（前置インクリメント）
c--;  // c = 6（後置デクリメント）
--c;  // c = 5（前置デクリメント）
```

### 比較演算子

```javascript
a == b;   // 等値（値が等しい）
a === b;  // 厳密等値（値と型が等しい）
a != b;   // 不等値
a !== b;  // 厳密不等値
a > b;    // より大きい
a >= b;   // 以上
a < b;    // より小さい
a <= b;   // 以下
```

### 論理演算子

```javascript
let x = true, y = false;

x && y;  // 論理AND（false）
x || y;  // 論理OR（true）
!x;      // 論理NOT（false）

// ショートサーキット評価
let obj = null;
let name = obj && obj.name;  // nullの場合エラーにならず、nameはnullになる

// Nullish Coalescing（ES2020）
let value = null;
let defaultValue = value ?? "デフォルト値";  // nullまたはundefinedの場合のみデフォルト値

// 論理代入演算子（ES2021）
let a = null;
a ||= "デフォルト値";  // a = a || "デフォルト値"
a &&= "新しい値";      // a = a && "新しい値"
a ??= "新しい値";      // a = a ?? "新しい値"
```

### ビット演算子

```javascript
let a = 5;  // 0101
let b = 3;  // 0011

a & b;    // 1（ビットAND: 0001）
a | b;    // 7（ビットOR: 0111）
a ^ b;    // 6（ビットXOR: 0110）
~a;       // -6（ビット反転）
a << 1;   // 10（左シフト: 1010）
a >> 1;   // 2（右シフト, 符号あり: 0010）
a >>> 1;  // 2（右シフト, 符号なし: 0010）
```

### 代入演算子

```javascript
let x = 10;

x += 5;   // x = x + 5;
x -= 5;   // x = x - 5;
x *= 5;   // x = x * 5;
x /= 5;   // x = x / 5;
x %= 5;   // x = x % 5;
x **= 5;  // x = x ** 5;
x &= 5;   // x = x & 5;
x |= 5;   // x = x | 5;
x ^= 5;   // x = x ^ 5;
x <<= 5;  // x = x << 5;
x >>= 5;  // x = x >> 5;
x >>>= 5; // x = x >>> 5;
```

### 条件（三項）演算子

```javascript
let age = 20;
let status = (age >= 18) ? "成人" : "未成年";
```

### Optional Chaining演算子（ES2020）

```javascript
let user = {
  address: {
    street: "山田町"
  }
};

// オプショナルチェーン（プロパティが存在しない場合はundefined）
let street1 = user.address?.street;       // "山田町"
let zipCode = user.address?.zipCode;      // undefined
let city = user.nonExistent?.city;        // undefined

// メソッド呼び出しにも使用可能
let result = object.method?.();
```

### その他の演算子

```javascript
// コンマ演算子
let x = (1, 2, 3);  // xは3

// delete演算子
let obj = { a: 1, b: 2 };
delete obj.a;  // { b: 2 }

// instanceof演算子
let arr = [];
arr instanceof Array;  // true

// in演算子
"length" in [];  // true

// void演算子
void 0;  // undefined

// typeof演算子
typeof "文字列";  // "string"
```

## 制御構造

### 条件文

```javascript
// if文
if (condition) {
  // 条件がtrueの場合の処理
} else if (anotherCondition) {
  // 別の条件がtrueの場合の処理
} else {
  // それ以外の場合の処理
}

// switch文
switch (expression) {
  case value1:
    // expression === value1の場合
    break;
  case value2:
    // expression === value2の場合
    break;
  default:
    // どのcaseにも一致しない場合
}
```

### ループ

```javascript
// for文
for (let i = 0; i < 5; i++) {
  console.log(i);
}

// for...in文（オブジェクトのプロパティを反復）
let obj = { a: 1, b: 2 };
for (let key in obj) {
  console.log(key, obj[key]);
}

// for...of文（イテラブルオブジェクトの値を反復）
let arr = [10, 20, 30];
for (let value of arr) {
  console.log(value);
}

// while文
let count = 0;
while (count < 5) {
  console.log(count);
  count++;
}

// do...while文
let i = 0;
do {
  console.log(i);
  i++;
} while (i < 5);
```

### 制御フロー

```javascript
// break - ループやswitch文を抜ける
for (let i = 0; i < 10; i++) {
  if (i === 5) break;
  console.log(i);  // 0, 1, 2, 3, 4
}

// continue - 現在の反復をスキップ
for (let i = 0; i < 5; i++) {
  if (i === 2) continue;
  console.log(i);  // 0, 1, 3, 4
}

// ラベル付きのbreak/continue
outerLoop: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    if (i === 1 && j === 1) break outerLoop;
    console.log(`i=${i}, j=${j}`);
  }
}
```

## 関数

### 関数宣言

```javascript
// 基本的な関数宣言
function greet(name) {
  return `こんにちは、${name}さん！`;
}

// 関数式
const greet = function(name) {
  return `こんにちは、${name}さん！`;
};

// アロー関数（ES6）
const greet = (name) => {
  return `こんにちは、${name}さん！`;
};

// アロー関数（短縮形）
const greet = name => `こんにちは、${name}さん！`;
const double = x => x * 2;
const getObject = () => ({ key: 'value' });
```

### パラメータ

```javascript
// デフォルトパラメータ
function greet(name = "ゲスト") {
  return `こんにちは、${name}さん！`;
}

// レストパラメータ
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}
sum(1, 2, 3, 4);  // 10

// 分割代入を使ったパラメータ
function processUser({ name, age, email }) {
  console.log(`${name}は${age}歳で、メールは${email}です`);
}
processUser({ name: "太郎", age: 30, email: "taro@example.com" });
```

### 関数の呼び出し

```javascript
// 通常の呼び出し
greet("太郎");

// call メソッド
greet.call(thisArg, "太郎");

// apply メソッド
greet.apply(thisArg, ["太郎"]);

// bind メソッド（thisを固定した新しい関数を作成）
const boundGreet = greet.bind(thisArg);
boundGreet("太郎");
```

### 即時実行関数式（IIFE）

```javascript
// 即時実行関数
(function() {
  let privateVar = "プライベート変数";
  console.log(privateVar);
})();

// パラメータ付き
(function(name) {
  console.log(`こんにちは、${name}さん！`);
})("太郎");

// アロー関数版
(() => {
  console.log("即時実行");
})();
```

### 高階関数

```javascript
// 関数を引数として受け取る
function executeOperation(operation, a, b) {
  return operation(a, b);
}

const add = (a, b) => a + b;
const multiply = (a, b) => a * b;

executeOperation(add, 5, 3);       // 8
executeOperation(multiply, 5, 3);  // 15

// 関数を返す
function createMultiplier(factor) {
  return function(number) {
    return number * factor;
  };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);
double(5);  // 10
triple(5);  // 15
```

### 再帰関数

```javascript
// 階乗計算の例
function factorial(n) {
  if (n <= 1) return 1;
  return n * factorial(n - 1);
}

factorial(5);  // 120
```

### クロージャ

```javascript
function createCounter() {
  let count = 0;
  return function() {
    return ++count;
  };
}

const counter = createCounter();
counter();  // 1
counter();  // 2
counter();  // 3
```

### Function.prototype.toString

```javascript
// 関数の文字列表現を取得
function add(a, b) {
  return a + b;
}

console.log(add.toString());
// "function add(a, b) {
//   return a + b;
// }"
```

## オブジェクト

### オブジェクトリテラル

```javascript
// 基本的なオブジェクト
const person = {
  firstName: "太郎",
  lastName: "山田",
  age: 30,
  
  // メソッド
  getFullName() {
    return `${this.lastName} ${this.firstName}`;
  }
};

// プロパティへのアクセス
console.log(person.firstName);  // "太郎"
console.log(person["lastName"]);  // "山田"

// 動的プロパティ名（ES6）
const propName = "age";
console.log(person[propName]);  // 30

// プロパティの追加
person.email = "taro@example.com";

// プロパティの削除
delete person.age;
```

### オブジェクトの作成

```javascript
// オブジェクトリテラル
const obj1 = { key: "value" };

// コンストラクタ関数
function Person(name, age) {
  this.name = name;
  this.age = age;
}
const person1 = new Person("太郎", 30);

// Object.create()
const prototype = { species: "human" };
const person2 = Object.create(prototype);
person2.name = "花子";

// クラス（ES6）
class Animal {
  constructor(name) {
    this.name = name;
  }
}
const dog = new Animal("ポチ");
```

### プロパティディスクリプタ

```javascript
const person = { name: "太郎" };

// プロパティディスクリプタの取得
Object.getOwnPropertyDescriptor(person, "name");
// { value: '太郎', writable: true, enumerable: true, configurable: true }

// プロパティの定義
Object.defineProperty(person, "age", {
  value: 30,
  writable: false,       // 値の変更を禁止
  enumerable: true,      // for...inなどで列挙可能
  configurable: true     // 再定義や削除が可能
});

// 複数プロパティの定義
Object.defineProperties(person, {
  height: { value: 175, writable: true },
  weight: { value: 70, writable: true }
});
```

### オブジェクトのプロパティとメソッド

```javascript
// 計算されたプロパティ名（ES6）
const propName = "dynamicKey";
const obj = {
  [propName]: "動的な値",
  [`computed_${propName}`]: "別の動的な値"
};

// ショートハンドプロパティ（ES6）
const name = "太郎";
const age = 30;
const person = { name, age };  // { name: "太郎", age: 30 }と同じ

// ショートハンドメソッド（ES6）
const calculator = {
  add(a, b) {
    return a + b;
  },
  subtract(a, b) {
    return a - b;
  }
};

// オブジェクトスプレッド（ES2018）
const defaults = { theme: "light", fontSize: 16 };
const userPrefs = { fontSize: 20 };
const merged = { ...defaults, ...userPrefs };  // { theme: "light", fontSize: 20 }
```

### Object.protortypeのメソッド

```javascript
const person = { name: "太郎", age: 30 };

person.hasOwnProperty("name");                // true
person.propertyIsEnumerable("name");          // true
Object.prototype.toString.call(person);       // "[object Object]"
Object.prototype.isPrototypeOf(person);       // false（継承関係がないため）
```

### オブジェクト操作

```javascript
const person = { name: "太郎", age: 30 };
const job = { title: "エンジニア", years: 5 };

// オブジェクトのマージ
const merged = Object.assign({}, person, job);
// または: const merged = { ...person, ...job };

// オブジェクトのコピー（シャローコピー）
const copy = Object.assign({}, person);
// または: const copy = { ...person };

// オブジェクトのキー、値、エントリーの取得
Object.keys(person);       // ["name", "age"]
Object.values(person);     // ["太郎", 30]
Object.entries(person);    // [["name", "太郎"], ["age", 30]]

// オブジェクトの凍結・シール
Object.freeze(person);     // オブジェクトを完全に不変にする
Object.isFrozen(person);   // true

Object.seal(person);       // 既存プロパティの設定変更のみ許可
Object.isSealed(person);   // true

Object.preventExtensions(person);  // 新規プロパティ追加を禁止
Object.isExtensible(person);       // false
```

### プロトタイプと継承

```javascript
// プロトタイプチェーン
const arr = [];
arr.__proto__ === Array.prototype;  // true
arr.__proto__.__proto__ === Object.prototype;  // true
arr.__proto__.__proto__.__proto__ === null;  // true

// プロトタイプを使った継承
function Animal(name) {
  this.name = name;
}
Animal.prototype.speak = function() {
  return `${this.name}が鳴く`;
};

function Dog(name, breed) {
  Animal.call(this, name);
  this.breed = breed;
}
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;
Dog.prototype.bark = function() {
  return `${this.name}が吠える: ワン！`;
};

const dog = new Dog("ポチ", "柴犬");
dog.speak();  // "ポチが鳴く"
dog.bark();   // "ポチが吠える: ワン！"
```

## 配列

### 配列の作成

```javascript
// 配列リテラル
const fruits = ["リンゴ", "バナナ", "オレンジ"];

// Array コンストラクタ
const numbers = new Array(1, 2, 3, 4, 5);
const emptyArray = new Array(5);  // 長さ5の空の配列

// Array.of() (ES6)
const items = Array.of(1, 2, 3);  // [1, 2, 3]

// Array.from() (ES6)
const arrayLike = { 0: "a", 1: "b", 2: "c", length: 3 };
const chars = Array.from(arrayLike);  // ["a", "b", "c"]
```

### 基本的なアクセスと操作

```javascript
const fruits = ["リンゴ", "バナナ", "オレンジ"];

// 要素へのアクセス
fruits[0];  // "リンゴ"
fruits[fruits.length - 1];  // "オレンジ"
fruits.at(-1);  // "オレンジ" (ES2022)

// 配列の長さ
fruits.length;  // 3

// 要素の追加
fruits.push("ブドウ");  // 末尾に追加
fruits.unshift("イチゴ");  // 先頭に追加

// 要素の削除
fruits.pop();  // 末尾から削除して返す
fruits.shift();  // 先頭から削除して返す

// 要素の置換
fruits[1] = "キウイ";
```

### 配列の変更メソッド

```javascript
const numbers = [1, 2, 3, 4, 5];

// splice - 要素の削除・置換・追加
numbers.splice(2, 1);  // [1, 2, 4, 5]
numbers.splice(2, 0, 3);  // [1, 2, 3, 4, 5]
numbers.splice(1, 2, "a", "b");  // [1, "a", "b", 4, 5]

// fill - 配列の要素を特定の値で埋める (ES6)
const filled = [1, 2, 3].fill(0);  // [0, 0, 0]
const partiallyFilled = [1, 2, 3, 4, 5].fill(0, 1, 3);  // [1, 0, 0, 4, 5]

// sort - 配列の並べ替え
const sorted = ["b", "c", "a"].sort();  // ["a", "b", "c"]
const numbersSorted = [10, 2, 5, 1].sort((a, b) => a - b);  // [1, 2, 5, 10]

// reverse - 配列の順序を反転
const reversed = [1, 2, 3].reverse();  // [3, 2, 1]

// copyWithin (ES6)
const copied = [1, 2, 3, 4, 5].copyWithin(0, 3, 5);  // [4, 5, 3, 4, 5]
```

### 配列の新しい配列を返すメソッド

```javascript
const numbers = [1, 2, 3, 4, 5];

// slice - 部分配列の取得
const sliced = numbers.slice(1, 4);  // [2, 3, 4]
const copied = numbers.slice();  // 配列全体のコピー

// concat - 配列の連結
const combined = [1, 2].concat([3, 4], 5);  // [1, 2, 3, 4, 5]
// または: const combined = [...[1, 2], ...[3, 4], 5];

// map - 各要素に関数を適用して新しい配列を作成
const doubled = numbers.map(x => x * 2);  // [2, 4, 6, 8, 10]

// filter - 条件に合う要素だけを含む新しい配列を作成
const evens = numbers.filter(x => x % 2 === 0);  // [2, 4]

// flat (ES2019) - ネストした配列をフラット化
const flattened = [1, [2, [3, 4]]].flat();  // [1, 2, [3, 4]]
const deepFlattened = [1, [2, [3, 4]]].flat(2);  // [1, 2, 3, 4]

// flatMap (ES2019) - mapしてからflatする
const flatMapped = [1, 2, 3].flatMap(x => [x, x * 2]);  // [1, 2, 2, 4, 3, 6]
```

### 検索と反復

```javascript
const numbers = [1, 2, 3, 4, 5];
const people = [
  { name: "Alice", age: 25 },
  { name: "Bob", age: 30 },
  { name: "Charlie", age: 35 }
];

// indexOf / lastIndexOf - 要素のインデックスを検索
numbers.indexOf(3);  // 2
numbers.lastIndexOf(3);  // 2

// includes - 要素が含まれているか確認
```