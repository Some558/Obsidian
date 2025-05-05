
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
numbers.includes(3); // true (ES2016)


// includes - 要素が含まれているか確認
// find / findIndex / findLast / findLastIndex - 条件に合う要素/インデックスを検索 numbers.find(x => x > 3); // 4 numbers.findIndex(x => x > 3); // 3 numbers.findLast(x => x < 4); // 3 (ES2022) numbers.findLastIndex(x => x < 4); // 2 (ES2022)

// some / every - 条件チェック numbers.some(x => x > 4); // true numbers.every(x => x > 0); // true

// forEach - 各要素に対して関数を実行 numbers.forEach(x => console.log(x));

// reduce / reduceRight - 要素を集約 const sum = numbers.reduce((acc, curr) => acc + curr, 0); // 15 const reversed = numbers.reduceRight((acc, curr) => [...acc, curr], []); // [5, 4, 3, 2, 1]

// entries / keys / values (ES6) Array.from(numbers.entries()); // [[0, 1], [1, 2], ...] Array.from(numbers.keys()); // [0, 1, 2, 3, 4] Array.from(numbers.values()); // [1, 2, 3, 4, 5]```



````

### 配列展開とスプレッド
```javascript
// 配列のスプレッド (ES6)
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const combined = [...arr1, ...arr2];  // [1, 2, 3, 4, 5, 6]

// 配列のコピー
const copy = [...arr1];  // [1, 2, 3]

// 配列要素の分割代入 (ES6)
const [first, second, ...rest] = [1, 2, 3, 4, 5];
console.log(first);  // 1
console.log(second);  // 2
console.log(rest);  // [3, 4, 5]
````

### TypedArray (型付き配列)

```javascript
// TypedArray - バイナリデータ操作
const int8Array = new Int8Array(4);  // 8ビット整数4つの配列
int8Array[0] = 42;

const float32Array = new Float32Array([1.1, 2.2, 3.3]);
float32Array[1] = 4.4;

// 利用可能なTypedArray
// Int8Array, Uint8Array, Uint8ClampedArray
// Int16Array, Uint16Array
// Int32Array, Uint32Array
// Float32Array, Float64Array
// BigInt64Array, BigUint64Array (ES2020)

// ArrayBuffer - 生のバイナリデータ
const buffer = new ArrayBuffer(16);  // 16バイトのバッファ
const view = new DataView(buffer);
view.setInt32(0, 42, true);  // リトルエンディアンで値をセット
view.getInt32(0, true);  // 42
```

## 文字列操作

### 文字列の作成

```javascript
// リテラル
const single = 'シングルクォート';
const double = "ダブルクォート";
const backtick = `バッククォート（テンプレートリテラル）`;

// テンプレートリテラル (ES6)
const name = "太郎";
const greeting = `こんにちは、${name}さん！`;

// 複数行文字列
const multiline = `これは
複数行の
文字列です。`;

// String コンストラクタ
const strFromNumber = String(42);  // "42"
```

### 文字列のアクセスと検索

```javascript
const str = "JavaScript";

// 文字へのアクセス
str.charAt(0);  // "J"
str[0];  // "J" (文字列はイミュータブルなので変更不可)
str.at(-1);  // "t" (ES2022)

// 部分文字列の検索
str.indexOf("Script");  // 4
str.lastIndexOf("a");  // 3
str.includes("Java");  // true (ES6)
str.startsWith("Java");  // true (ES6)
str.endsWith("Script");  // true (ES6)
str.search(/Script/);  // 4（正規表現使用）
```

### 部分文字列の抽出

```javascript
const str = "JavaScript";

// 部分文字列の取得
str.substring(0, 4);  // "Java"
str.slice(4);  // "Script"
str.slice(-6);  // "Script"
str.slice(0, -6);  // "Java"

// 文字列の分割
str.split("");  // ["J", "a", "v", "a", "S", "c", "r", "i", "p", "t"]
str.split("a");  // ["J", "v", "Script"]
"apple,orange,banana".split(",");  // ["apple", "orange", "banana"]
```

### 文字列の変換

```javascript
const str = "  Hello, World!  ";

// 大文字・小文字変換
str.toLowerCase();  // "  hello, world!  "
str.toUpperCase();  // "  HELLO, WORLD!  "

// 空白の削除
str.trim();  // "Hello, World!"
str.trimStart();  // "Hello, World!  " (ES2019)
str.trimEnd();  // "  Hello, World!" (ES2019)

// パディング (ES2017)
"42".padStart(5, "0");  // "00042"
"42".padEnd(5, "0");  // "42000"

// 文字列の置換
"hello".replace("l", "L");  // "heLlo" (最初の一致のみ)
"hello".replaceAll("l", "L");  // "heLLo" (ES2021)

// 正規表現での置換
"hello".replace(/l/g, "L");  // "heLLo"
```

### その他の文字列メソッド

```javascript
// 文字列の繰り返し (ES6)
"abc".repeat(3);  // "abcabcabc"

// コードポイント操作
"😀".codePointAt(0);  // 128512
String.fromCodePoint(128512);  // "😀"

// 生文字列表記 (raw strings) (ES6)
String.raw`line1\nline2`;  // "line1\nline2" (\nはエスケープされない)

// 文字列比較
"a".localeCompare("b");  // -1
"b".localeCompare("a");  // 1
"a".localeCompare("a");  // 0

// 文字列結合
"Hello, " + "World!";  // "Hello, World!"
"".concat("Hello", ", ", "World!");  // "Hello, World!"
```

## 日付と時間

### Date オブジェクト

```javascript
// 現在の日時
const now = new Date();

// 特定の日時
const date1 = new Date("2023-01-15T12:30:00");
const date2 = new Date(2023, 0, 15, 12, 30, 0); // 月は0から始まる (0=1月)
const timestamp = new Date(1673789400000); // タイムスタンプ（ミリ秒）

// タイムスタンプの取得
now.getTime();  // 1673789400000
Date.now();     // 現在のタイムスタンプ

// 日付コンポーネントの取得（ローカル時間）
now.getFullYear();    // 2023
now.getMonth();       // 0 (1月)
now.getDate();        // 15
now.getDay();         // 0 (日曜日) から 6 (土曜日)
now.getHours();       // 12
now.getMinutes();     // 30
now.getSeconds();     // 0
now.getMilliseconds(); // 0

// 日付コンポーネントの取得（UTC）
now.getUTCFullYear();
now.getUTCMonth();
// 他のUTCメソッド...

// 日付コンポーネントの設定
now.setFullYear(2024);
now.setMonth(11);     // 12月
now.setDate(31);
// 他のsetメソッド...

// 日付の文字列表現
now.toString();           // "Sun Jan 15 2023 12:30:00 GMT+0900 (日本標準時)"
now.toDateString();       // "Sun Jan 15 2023"
now.toTimeString();       // "12:30:00 GMT+0900 (日本標準時)"
now.toISOString();        // "2023-01-15T03:30:00.000Z" (ISO 8601)
now.toUTCString();        // "Sun, 15 Jan 2023 03:30:00 GMT"
now.toLocaleDateString(); // "2023/1/15"
now.toLocaleTimeString(); // "12:30:00"
now.toLocaleString();     // "2023/1/15 12:30:00"

// 日付の比較
const date1 = new Date(2023, 0, 1);
const date2 = new Date(2023, 11, 31);
date1 < date2;  // true
date1 > date2;  // false
date1.getTime() === date2.getTime();  // false
```

### Intl.DateTimeFormat (国際化)

```javascript
// 日付の国際化フォーマット
const date = new Date(2023, 0, 15, 12, 30, 0);

// ロケールと表示オプション
const japaneseDate = new Intl.DateTimeFormat("ja-JP", {
  year: "numeric",
  month: "long",
  day: "numeric",
  weekday: "long",
  hour: "numeric",
  minute: "numeric",
  timeZone: "Asia/Tokyo"
}).format(date);
// "2023年1月15日日曜日 12時30分"

// 相対時間フォーマット (Intl.RelativeTimeFormat)
const rtf = new Intl.RelativeTimeFormat("ja", { numeric: "auto" });
rtf.format(-1, "day");    // "昨日"
rtf.format(2, "day");     // "明後日"
rtf.format(-30, "minute"); // "30分前"
```

### パフォーマンス計測

```javascript
// 高精度タイマー
const start = performance.now();
// 何らかの処理
const end = performance.now();
console.log(`処理時間: ${end - start} ミリ秒`);
```

## 正規表現

### 正規表現の作成

```javascript
// リテラル構文
const regex1 = /pattern/flags;

// RegExp コンストラクタ
const regex2 = new RegExp("pattern", "flags");
```

### フラグ

```javascript
/pattern/g;    // グローバルマッチ（すべての一致を検索）
/pattern/i;    // 大文字小文字を区別しない
/pattern/m;    // 複数行モード（^と$が各行の先頭と末尾にマッチ）
/pattern/s;    // .が改行にもマッチ（dotAll モード）(ES2018)
/pattern/u;    // Unicodeモード（Unicode コードポイントを扱う）(ES6)
/pattern/y;    // sticky モード（lastIndexから検索開始）(ES6)
/pattern/d;    // インデックスを含む結果 (ES2022)
```

### パターン構文

```javascript
// 文字クラス
/[abc]/;        // a, b, または c
/[^abc]/;       // a, b, c 以外の文字
/[a-z]/;        // a から z までの文字
/\d/;           // 数字 ([0-9] と同等)
/\D/;           // 数字以外 ([^0-9] と同等)
/\w/;           // 単語文字 ([A-Za-z0-9_] と同等)
/\W/;           // 単語文字以外
/\s/;           // 空白文字（スペース、タブ、改行など）
/\S/;           // 空白文字以外

// アンカー
/^start/;       // 文字列（または行）の先頭にマッチ
/end$/;         // 文字列（または行）の末尾にマッチ
/\bword\b/;     // 単語境界

// 量指定子
/a*/;           // 0回以上の繰り返し
/a+/;           // 1回以上の繰り返し
/a?/;           // 0回または1回
/a{3}/;         // 3回の繰り返し
/a{3,}/;        // 3回以上の繰り返し
/a{3,5}/;       // 3回以上5回以下の繰り返し

// グループ化と参照
/(abc)/;        // グループ化
/(?:abc)/;      // 非キャプチャグループ
/\1/;           // 最初のグループへの後方参照
/(?<name>abc)/; // 名前付きキャプチャグループ (ES2018)
/\k<name>/;     // 名前付きグループへの後方参照 (ES2018)

// 先読み/後読みアサーション
/a(?=b)/;       // 正の先読み（aの後にbが続く場合のみaにマッチ）
/a(?!b)/;       // 否定の先読み（aの後にbが続かない場合のみaにマッチ）
/(?<=b)a/;      // 正の後読み（bの後のaにのみマッチ）(ES2018)
/(?<!b)a/;      // 否定の後読み（bの後ではないaにのみマッチ）(ES2018)

// その他
/a|b/;          // 選言（aまたはb）
/./;            // 改行を除く任意の1文字
/\p{Script=Hiragana}/u;  // Unicode プロパティエスケープ（ひらがな）(ES2018)
```

### 正規表現のメソッド

```javascript
const str = "Hello, world!";
const regex = /world/;

// test - パターンが一致するか確認
regex.test(str);  // true

// exec - マッチング情報を取得
regex.exec(str);  // ["world", index: 7, input: "Hello, world!", groups: undefined]

// matchAll - すべての一致を取得 (ES2020)
const regexGlobal = /o/g;
Array.from(str.matchAll(regexGlobal));
// [["o", index: 4, ...], ["o", index: 8, ...]]

// マッチしたインデックスを取得 (ES2022)
const matchWithIndices = /o/d.exec("Hello");
matchWithIndices.indices[0];  // [4, 5]

// 文字列のマッチメソッド
str.match(regex);        // ["world"]
str.match(/o/g);         // ["o", "o"]
str.search(regex);       // 7（最初の一致のインデックス）
str.replace(regex, "JavaScript");  // "Hello, JavaScript!"
str.replaceAll(/[aeiou]/g, "*");   // "H*ll*, w*rld!" (ES2021)
str.split(/\s*,\s*/);   // ["Hello", "world!"]
```

## エラー処理

### 例外処理

```javascript
// try...catch...finally
try {
  // エラーが発生する可能性のあるコード
  throw new Error("エラーが発生しました");
} catch (error) {
  // エラーハンドリング
  console.error(error.name);     // "Error"
  console.error(error.message);  // "エラーが発生しました"
  console.error(error.stack);    // スタックトレース
} finally {
  // エラーの有無にかかわらず実行されるコード
  console.log("この処理は必ず実行されます");
}

// catch節のオプショナルバインディング (ES2019)
try {
  throw new SyntaxError("構文エラー");
} catch {  // エラーオブジェクトが不要な場合
  console.log("エラーをキャッチしました");
}
```

### エラーの種類

```javascript
// 組み込みエラー型
throw new Error("一般的なエラー");
throw new SyntaxError("構文エラー");
throw new ReferenceError("参照エラー");
throw new TypeError("型エラー");
throw new RangeError("範囲エラー");
throw new URIError("URIエラー");
throw new EvalError("eval()エラー");
throw new AggregateError([error1, error2], "複合エラー"); // ES2021

// カスタムエラー
class CustomError extends Error {
  constructor(message) {
    super(message);
    this.name = "CustomError";
    this.date = new Date();
  }
}

throw new CustomError("カスタムエラーが発生しました");
```

### エラー伝播

```javascript
// エラーの再スロー
try {
  throw new Error("元のエラー");
} catch (error) {
  console.error("エラーを処理しています...");
  throw error;  // エラーを上位ハンドラに伝播
}

// エラーチェーン
try {
  throw new Error("元のエラー");
} catch (originalError) {
  throw new Error("新しいエラー", { cause: originalError });  // ES2022
}
```

## 非同期処理

### コールバック

```javascript
// コールバックパターン
function fetchData(url, callback) {
  // データ取得後にコールバックを実行
  setTimeout(() => {
    const data = { result: "サンプルデータ" };
    callback(null, data);
  }, 1000);
}

fetchData("https://example.com/api", (error, data) => {
  if (error) {
    console.error("エラー:", error);
    return;
  }
  console.log("データ:", data);
});
```

### Promise

```javascript
// Promiseの作成
const promise = new Promise((resolve, reject) => {
  // 非同期処理
  const success = true;
  if (success) {
    resolve("処理が成功しました");
  } else {
    reject(new Error("処理が失敗しました"));
  }
});

// Promiseの使用
promise
  .then(result => {
    console.log(result);  // "処理が成功しました"
    return result.toUpperCase();
  })
  .then(upperResult => {
    console.log(upperResult);  // "処理が成功しました"
  })
  .catch(error => {
    console.error("エラー:", error);
  })
  .finally(() => {
    console.log("終了処理");
  });

// Promise静的メソッド
Promise.resolve(42);  // 解決済みのPromise
Promise.reject(new Error("拒否"));  // 拒否されたPromise

// 複数のPromiseの処理
Promise.all([promise1, promise2, promise3])  // すべて解決したら結果の配列を返す
  .then(results => console.log(results))
  .catch(error => console.error(error));  // 1つでも拒否されたら最初のエラーを返す

Promise.race([promise1, promise2])  // 最初に解決/拒否したPromiseの結果を返す
  .then(result => console.log(result))
  .catch(error => console.error(error));

Promise.allSettled([promise1, promise2])  // すべてのPromiseが完了したら状態と値/理由を返す (ES2020)
  .then(results => console.log(results));

Promise.any([promise1, promise2])  // 最初に解決したPromiseの結果を返す (ES2021)
  .then(result => console.log(result))
  .catch(error => console.error(error));  // すべて拒否されたらAggregateErrorを返す
```

### async/await

```javascript
// async関数
async function fetchData() {
  try {
    const response = await fetch("https://example.com/api");
    if (!response.ok) {
      throw new Error("ネットワークレスポンスが正常ではありません");
    }
    const data = await response.json();
    return data;
  } catch (error) {
    console.error("データの取得に失敗しました:", error);
    throw error;  // エラーを再スロー
  }
}

// async関数の使用
fetchData()
  .then(data => console.log("データ:", data))
  .catch(error => console.error("エラー:", error));

// アロー関数でのasync
const getData = async () => {
  // ...
};

// クラスメソッドでのasync
class DataService {
  async fetchData() {
    // ...
  }
}

// 並列処理
async function fetchMultipleData() {
  // 並列に実行
  const [data1, data2] = await Promise.all([
    fetch("https://example.com/api/1").then(res => res.json()),
    fetch("https://example.com/api/2").then(res => res.json())
  ]);
  return { data1, data2 };
}

// for await...of（イテラブルなPromiseを反復）(ES2018)
async function processChunks() {
  const stream = getReadableStreamSomehow();
  for await (const chunk of stream) {
    console.log(chunk);
  }
}
```

### AbortController

```javascript
// 非同期処理のキャンセル
const controller = new AbortController();
const signal = controller.signal;

fetch("https://example.com/api", { signal })
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => {
    if (error.name === "AbortError") {
      console.log("フェッチ操作がキャンセルされました");
    } else {
      console.error("エラー:", error);
    }
  });

// 1秒後にリクエストをキャンセル
setTimeout(() => {
  controller.abort();
}, 1000);
```

## モジュール

### ES Modules

```javascript
// export
// math.js
export const PI = 3.14159;
export function add(a, b) {
  return a + b;
}
export class Calculator {
  // ...
}

// デフォルトエクスポート
export default function multiply(a, b) {
  return a * b;
}

// import
// app.js
import multiply, { PI, add, Calculator } from './math.js';
import * as math from './math.js';

console.log(PI);           // 3.14159
console.log(add(2, 3));    // 5
console.log(multiply(2, 3)); // 6
console.log(math.PI);      // 3.14159

// 動的インポート (ES2020)
import('./module.js')
  .then(module => {
    console.log(module.default);
  })
  .catch(error => {
    console.error("モジュールのロードに失敗:", error);
  });

// async/awaitでの動的インポート
async function loadModule() {
  const module = await import('./module.js');
  return module.default;
}
```

### モジュール集約と再エクスポート

```javascript
// モジュールの集約と再エクスポート
// lib.js
export { default as func1 } from './module1.js';
export { func2, func3 } from './module2.js';
export * from './module3.js';
export * as namespace from './module4.js';

// 名前の変更
import { original as alias } from './module.js';
export { original as alias } from './module.js';
```

### モジュールの属性

```javascript
// JSON モジュール (提案中)
import data from './data.json' assert { type: 'json' };

// CSS モジュール (提案中)
import styles from './styles.css' assert { type: 'css' };
```

## DOM操作

### 要素の選択

```javascript
// ID による選択
const element = document.getElementById('myId');

// クラスによる選択
const elements = document.getElementsByClassName('myClass');

// タグ名による選択
const divs = document.getElementsByTagName('div');

// CSSセレクタによる選択（最初の一致）
const element = document.querySelector('.myClass');

// CSSセレクタによる選択（すべての一致）
const elements = document.querySelectorAll('div.item');

// 属性による選択
const elements = document.querySelectorAll('[data-type="example"]');

// 子孫要素の選択
const childElements = parentElement.querySelectorAll('.child');
```

### DOM要素の作成と操作

```javascript
// 新しい要素の作成
const div = document.createElement('div');
const textNode = document.createTextNode('テキスト');

// 要素の属性設定
div.id = 'newDiv';
div.className = 'container';
div.setAttribute('data-value', '42');
div.setAttribute('aria-label', 'コンテナ');

// データ属性
div.dataset.value = '42';  // data-value="42" に相当

// スタイル操作
div.style.color = 'red';
div.style.fontSize = '16px';
div.style.backgroundColor = '#f0f0f0';

// クラス操作
div.classList.add('active');
div.classList.remove('hidden');
div.classList.toggle('visible');
div.classList.replace('old', 'new');
div.classList.contains('active');  // true/false

// コンテンツ操作
div.textContent = 'テキストコンテンツ';
div.innerHTML = '<span>HTMLコンテンツ</span>';
div.innerText = 'テキスト（非表示要素を除く）';

// アウターHTML
element.outerHTML = '<div>新しい要素</div>';
```

### DOM構造の操作

```javascript
// ノードの追加
parent.appendChild(child);
parent.append(child1, child2, 'テキスト');  // 複数追加可能
parent.prepend(child);  // 先頭に追加

// ノードの挿入
parent.insertBefore(newNode, referenceNode);
referenceNode.before(newNode);  // 前に挿入
referenceNode.after(newNode);   // 後に挿入

// ノードの置換
parent.replaceChild(newNode, oldNode);
oldNode.replaceWith(newNode);

// ノードの削除
parent.removeChild(child);
child.remove();

// ノードのクローン
const clone = node.cloneNode(true);  // trueで深いクローン（子孫も含む）
```

### DOMイベント

```javascript
// イベントリスナーの追加
element.addEventListener('click', (event) => {
  console.log('クリックされました');
});

// オプション付きのイベントリスナー
element.addEventListener('click', handler, {
  once: true,         // 1回だけ実行
  passive: true,      // デフォルトのブラウザ動作を妨げない
  capture: false      // イベント伝播のフェーズ（キャプチャまたはバブリング）
});

// イベントリスナーの削除
element.removeEventListener('click', handler);

// イベントの作成とディスパッチ
const event = new Event('build');
element.dispatchEvent(event);

// カスタムイベント
const event = new CustomEvent('product-select', {
  detail: { productId: 123 }
});
element.dispatchEvent(event);
```

### DOMプロパティとメソッド

````javascript
// ノードプロパティ
element.nodeName;     // タグ名（大文字）
element.nodeType;     // ノードタイプ（1=要素、3=テキストなど）
element.nodeValue;    // ノードの値

// 親子関係の取得
element.parentNode;
element.parentElement;
element.childNodes;   // すべての子ノード（含テキストノード）
element.children;     // 子要素ノードのみ
element.firstChild;
element.lastChild;
element.firstElementChild;
element.lastElementChild;

// 兄弟関係の取得
element.previousSibling;
element.nextSibling;
element.previousElementSibling;
element.nextElementSibling;

// 寸法と位置
element.getBoundingClientRect();  // 要素の位置と寸法
element.clientWidth;   // パディングを含む幅（ボーダー、スクロールバーを除く）
element.clientHeight;  // パディングを含む高さ
element.offsetWidth;   // ボーダーと# JavaScript 詳細チートシート (ES2022+)

## 目次

1. [基本構文](#基本構文)
2. [変数と定数](#変数と定数)
3. [データ型](#データ型)
4. [演算子](#演算子)
5. [制御構造](#制御構造)
6. [関数](#関数)
7. [オブジェクト](#オブジェクト)
8. [配列](#配列)
9. [文字列操作](#文字列操作)
10. [日付と時間](#日付と時間)
11. [正規表現](#正規表現)
12. [エラー処理](#エラー処理)
13. [非同期処理](#非同期処理)
14. [モジュール](#モジュール)
15. [DOM操作](#dom操作)
16. [イベント処理](#イベント処理)
17. [Fetch APIとAjax](#fetch-apiとajax)
18. [ローカルストレージ](#ローカルストレージ)
19. [クラス](#クラス)
20. [イテレータとジェネレータ](#イテレータとジェネレータ)
21. [高階関数](#高階関数)
22. [デストラクチャリング](#デストラクチャリング)
23. [スプレッド構文とレスト構文](#スプレッド構文とレスト構文)
24. [プロキシとリフレクション](#プロキシとリフレクション)
25. [Web API](#web-api)
26. [ES2022以降の新機能](#es2022以降の新機能)
27. [デバッグとパフォーマンス](#デバッグとパフォーマンス)

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
````

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