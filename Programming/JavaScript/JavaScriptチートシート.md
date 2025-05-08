# JavaScript基本チートシート

## 目次

1. [変数宣言](https://claude.ai/chat/e865ea32-0e63-4ca7-868c-4e549ebd2217#%E5%A4%89%E6%95%B0%E5%AE%A3%E8%A8%80)
2. [データ型](https://claude.ai/chat/e865ea32-0e63-4ca7-868c-4e549ebd2217#%E3%83%87%E3%83%BC%E3%82%BF%E5%9E%8B)
3. [演算子](https://claude.ai/chat/e865ea32-0e63-4ca7-868c-4e549ebd2217#%E6%BC%94%E7%AE%97%E5%AD%90)
4. [条件文](https://claude.ai/chat/e865ea32-0e63-4ca7-868c-4e549ebd2217#%E6%9D%A1%E4%BB%B6%E6%96%87)
5. [ループ](https://claude.ai/chat/e865ea32-0e63-4ca7-868c-4e549ebd2217#%E3%83%AB%E3%83%BC%E3%83%97)
6. [関数](https://claude.ai/chat/e865ea32-0e63-4ca7-868c-4e549ebd2217#%E9%96%A2%E6%95%B0)
7. [配列](https://claude.ai/chat/e865ea32-0e63-4ca7-868c-4e549ebd2217#%E9%85%8D%E5%88%97)
8. [オブジェクト](https://claude.ai/chat/e865ea32-0e63-4ca7-868c-4e549ebd2217#%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)
9. [DOM操作](https://claude.ai/chat/e865ea32-0e63-4ca7-868c-4e549ebd2217#dom%E6%93%8D%E4%BD%9C)
10. [イベント処理](https://claude.ai/chat/e865ea32-0e63-4ca7-868c-4e549ebd2217#%E3%82%A4%E3%83%99%E3%83%B3%E3%83%88%E5%87%A6%E7%90%86)
11. [非同期処理](https://claude.ai/chat/e865ea32-0e63-4ca7-868c-4e549ebd2217#%E9%9D%9E%E5%90%8C%E6%9C%9F%E5%87%A6%E7%90%86)
12. [エラー処理](https://claude.ai/chat/e865ea32-0e63-4ca7-868c-4e549ebd2217#%E3%82%A8%E3%83%A9%E3%83%BC%E5%87%A6%E7%90%86)

## 変数宣言

JavaScriptには3種類の変数宣言方法があります。

```javascript
// let - 再代入可能な変数（ブロックスコープ）
let count = 1;
count = 2; // 再代入可能

// const - 定数（再代入不可、ブロックスコープ）
const PI = 3.14;
// PI = 3.141592; // エラー: 再代入不可

// var - 旧式の変数宣言（関数スコープ）
var name = "JavaScript";
name = "JS"; // 再代入可能
```

**使用事例:**

```javascript
// 年齢を計算する
const birthYear = 1990;
let currentYear = 2025;
let age = currentYear - birthYear;
console.log(`年齢は${age}歳です`); // 年齢は35歳です
```

## データ型

JavaScriptの基本データ型です。

```javascript
// プリミティブ型
let str = "文字列";           // 文字列 (String)
let num = 42;                // 数値 (Number)
let bool = true;             // 真偽値 (Boolean)
let nothing = null;          // null
let undef = undefined;       // undefined
let bigInt = 9007199254740991n; // BigInt
let sym = Symbol("id");      // Symbol

// 参照型
let arr = [1, 2, 3];         // 配列 (Array)
let obj = { name: "太郎" };   // オブジェクト (Object)
let func = function() {};    // 関数 (Function)
```

**使用事例:**

```javascript
// データ型のチェック
console.log(typeof "こんにちは");  // "string"
console.log(typeof 42);           // "number"
console.log(typeof true);         // "boolean"
console.log(typeof [1, 2, 3]);    // "object" (配列もオブジェクト)
console.log(Array.isArray([1, 2, 3])); // true (配列かどうかの確認)
```

## 演算子

基本的な演算子の一覧です。

```javascript
// 算術演算子
let sum = 5 + 3;         // 加算: 8
let diff = 10 - 4;       // 減算: 6
let product = 3 * 4;     // 乗算: 12
let quotient = 10 / 2;   // 除算: 5
let remainder = 10 % 3;  // 剰余: 1
let power = 2 ** 3;      // べき乗: 8

// インクリメント/デクリメント
let i = 1;
i++;                     // 後置インクリメント: i = 2
++i;                     // 前置インクリメント: i = 3
i--;                     // 後置デクリメント: i = 2
--i;                     // 前置デクリメント: i = 1

// 代入演算子
let x = 5;
x += 3;                  // x = x + 3: 8
x -= 2;                  // x = x - 2: 6
x *= 2;                  // x = x * 2: 12
x /= 4;                  // x = x / 4: 3
x %= 2;                  // x = x % 2: 1

// 比較演算子
let a = 5, b = "5";
console.log(a == b);     // 等価 (値の比較): true
console.log(a === b);    // 厳密等価 (値と型の比較): false
console.log(a != b);     // 不等価: false
console.log(a !== b);    // 厳密不等価: true
console.log(a > 3);      // より大きい: true
console.log(a <= 5);     // 以下: true

// 論理演算子
let t = true, f = false;
console.log(t && f);     // 論理AND: false
console.log(t || f);     // 論理OR: true
console.log(!t);         // 論理NOT: false

// 三項演算子
let age = 20;
let status = age >= 18 ? "成人" : "未成年";  // "成人"
```

**使用事例:**

```javascript
// 割引価格の計算
const price = 1000;
const discount = 0.2;  // 20%割引
const finalPrice = price - (price * discount);
console.log(`最終価格: ${finalPrice}円`);  // 最終価格: 800円

// 合格判定
const score = 75;
const result = score >= 60 ? "合格" : "不合格";
console.log(result);  // 合格
```

## 条件文

条件に基づいて処理を分岐させます。

```javascript
// if文
let age = 18;

if (age >= 20) {
    console.log("成人です");
} else if (age >= 18) {
    console.log("18歳以上です");
} else {
    console.log("未成年です");
}

// switch文
let day = "月曜日";

switch (day) {
    case "月曜日":
        console.log("仕事始め");
        break;
    case "水曜日":
        console.log("週の真ん中");
        break;
    case "金曜日":
        console.log("もうすぐ週末");
        break;
    case "土曜日":
    case "日曜日":
        console.log("週末です");
        break;
    default:
        console.log("平日です");
        break;
}
```

**使用事例:**

```javascript
// 季節判定
function getSeason(month) {
    if (month >= 3 && month <= 5) {
        return "春";
    } else if (month >= 6 && month <= 8) {
        return "夏";
    } else if (month >= 9 && month <= 11) {
        return "秋";
    } else {
        return "冬";
    }
}

console.log(getSeason(4));  // 春
```

## ループ

繰り返し処理を行います。

```javascript
// for ループ
for (let i = 0; i < 5; i++) {
    console.log(i);  // 0, 1, 2, 3, 4
}

// while ループ
let count = 0;
while (count < 3) {
    console.log(count);  // 0, 1, 2
    count++;
}

// do-while ループ（最低1回は実行）
let j = 0;
do {
    console.log(j);  // 0
    j++;
} while (j < 1);

// for...of ループ（配列や反復可能オブジェクト用）
const colors = ["赤", "青", "緑"];
for (const color of colors) {
    console.log(color);  // 赤, 青, 緑
}

// for...in ループ（オブジェクトのプロパティ用）
const person = { name: "太郎", age: 30 };
for (const key in person) {
    console.log(`${key}: ${person[key]}`);  // name: 太郎, age: 30
}
```

**使用事例:**

```javascript
// 1から10までの合計を計算
let sum = 0;
for (let i = 1; i <= 10; i++) {
    sum += i;
}
console.log(`合計: ${sum}`);  // 合計: 55

// 配列の要素を処理
const numbers = [1, 2, 3, 4, 5];
let total = 0;
for (const num of numbers) {
    total += num;
}
console.log(`配列の合計: ${total}`);  // 配列の合計: 15
```

## 関数

再利用可能なコードブロックを定義します。

```javascript
// 関数宣言
function greet(name) {
    return `こんにちは、${name}さん！`;
}

// 関数式
const add = function(a, b) {
    return a + b;
};

// アロー関数
const multiply = (a, b) => a * b;

// デフォルトパラメータ
function welcome(name = "ゲスト") {
    return `ようこそ、${name}さん！`;
}

// 可変長引数
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}
```

**使用事例:**

```javascript
// 関数の使用
console.log(greet("花子"));  // こんにちは、花子さん！
console.log(add(5, 3));      // 8
console.log(multiply(4, 2)); // 8
console.log(welcome());      // ようこそ、ゲストさん！
console.log(sum(1, 2, 3, 4, 5)); // 15

// コールバック関数
function processData(data, callback) {
    // データを処理
    const result = `処理済み: ${data}`;
    // 処理が完了したらコールバックを実行
    callback(result);
}

processData("テストデータ", function(result) {
    console.log(result); // 処理済み: テストデータ
});
```

## 配列

複数の値をまとめて格納します。

```javascript
// 配列の作成
const fruits = ["りんご", "バナナ", "オレンジ"];

// 配列へのアクセス
console.log(fruits[0]);  // りんご
console.log(fruits.length);  // 3

// 配列の操作
fruits.push("ぶどう");    // 末尾に追加
fruits.pop();            // 末尾を削除して返す
fruits.unshift("いちご"); // 先頭に追加
fruits.shift();          // 先頭を削除して返す
fruits.splice(1, 1, "キウイ"); // インデックス1の要素を削除して"キウイ"を挿入

// 配列のメソッド
const numbers = [1, 2, 3, 4, 5];

// map: 各要素に関数を適用して新しい配列を作成
const doubled = numbers.map(num => num * 2);  // [2, 4, 6, 8, 10]

// filter: 条件に合う要素だけの新しい配列を作成
const evens = numbers.filter(num => num % 2 === 0);  // [2, 4]

// reduce: 配列を単一の値に集約
const sum = numbers.reduce((acc, num) => acc + num, 0);  // 15

// forEach: 各要素に対して関数を実行
numbers.forEach(num => console.log(num));
```

**使用事例:**

```javascript
// 商品リストの合計金額を計算
const products = [
    { name: "本", price: 1200 },
    { name: "ペン", price: 300 },
    { name: "ノート", price: 500 }
];

const totalPrice = products.reduce((sum, product) => sum + product.price, 0);
console.log(`合計金額: ${totalPrice}円`);  // 合計金額: 2000円

// 名前のリストからイニシャルを抽出
const names = ["山田 太郎", "鈴木 花子", "佐藤 次郎"];
const initials = names.map(name => {
    const parts = name.split(" ");
    return `${parts[0][0]}.${parts[1][0]}`;
});
console.log(initials);  // ["山.太", "鈴.花", "佐.次"]
```

## オブジェクト

キーと値のペアを格納する構造です。

```javascript
// オブジェクトの作成
const person = {
    firstName: "太郎",
    lastName: "山田",
    age: 30,
    greet: function() {
        return `こんにちは、${this.lastName} ${this.firstName}です。`;
    }
};

// プロパティへのアクセス
console.log(person.firstName);  // 太郎
console.log(person["lastName"]); // 山田

// メソッドの呼び出し
console.log(person.greet());  // こんにちは、山田 太郎です。

// プロパティの追加と変更
person.email = "taro@example.com";  // 新しいプロパティを追加
person.age = 31;  // 既存のプロパティを変更

// プロパティの削除
delete person.email;

// オブジェクトのメソッド
const keys = Object.keys(person);  // ["firstName", "lastName", "age", "greet"]
const values = Object.values(person);  // ["太郎", "山田", 31, [Function: greet]]
const entries = Object.entries(person);  // [["firstName", "太郎"], ["lastName", "山田"], ...]

// オブジェクトのコピー
const personCopy = Object.assign({}, person);  // 浅いコピー
const personCopy2 = { ...person };  // スプレッド構文での浅いコピー
```

**使用事例:**

```javascript
// 学生データの管理
const student = {
    id: "S001",
    name: "佐藤 花子",
    scores: {
        math: 85,
        english: 90,
        science: 78
    },
    getAverage: function() {
        const scores = Object.values(this.scores);
        const sum = scores.reduce((total, score) => total + score, 0);
        return sum / scores.length;
    }
};

console.log(`平均点: ${student.getAverage()}`);  // 平均点: 84.33...

// オブジェクトの配列の操作
const employees = [
    { id: 1, name: "田中 一郎", department: "営業" },
    { id: 2, name: "鈴木 二郎", department: "開発" },
    { id: 3, name: "佐藤 三郎", department: "営業" }
];

const salesStaff = employees.filter(emp => emp.department === "営業");
console.log(salesStaff);  // [{ id: 1, name: "田中 一郎", ... }, { id: 3, name: "佐藤 三郎", ... }]
```

## DOM操作

HTMLドキュメントを操作します。

```javascript
// 要素の取得
const element = document.getElementById("myId");
const elements = document.getElementsByClassName("myClass");
const tags = document.getElementsByTagName("div");
const selector = document.querySelector(".myClass");
const selectorAll = document.querySelectorAll("p");

// 要素の作成と追加
const newDiv = document.createElement("div");
newDiv.textContent = "新しい要素";
document.body.appendChild(newDiv);

// 要素の変更
element.textContent = "テキスト内容";
element.innerHTML = "<span>HTMLコンテンツ</span>";
element.setAttribute("class", "newClass");
element.style.color = "red";
element.classList.add("active");
element.classList.remove("inactive");
element.classList.toggle("visible");

// 要素の削除
const parent = document.getElementById("parent");
const child = document.getElementById("child");
parent.removeChild(child);
// または
child.remove();
```

**使用事例:**

```javascript
// ボタンクリック時に新しいリスト項目を追加
document.getElementById("addButton").addEventListener("click", function() {
    // 新しいリスト項目の作成
    const newItem = document.createElement("li");
    newItem.textContent = "新しい項目";
    
    // リストに追加
    document.getElementById("myList").appendChild(newItem);
});

// フォームデータの検証
document.getElementById("myForm").addEventListener("submit", function(event) {
    const nameInput = document.getElementById("name");
    
    if (nameInput.value.trim() === "") {
        // 入力が空の場合
        event.preventDefault();  // フォーム送信を中止
        document.getElementById("nameError").textContent = "名前を入力してください";
        nameInput.classList.add("error");
    }
});
```

## イベント処理

ユーザー操作などのイベントに応答します。

```javascript
// イベントリスナーの追加
const button = document.getElementById("myButton");
button.addEventListener("click", function(event) {
    console.log("ボタンがクリックされました");
    console.log(event);  // イベントオブジェクト
});

// イベントリスナーの削除
function handleClick() {
    console.log("クリック処理");
}
button.addEventListener("click", handleClick);
button.removeEventListener("click", handleClick);

// 主なイベントタイプ
/*
click - クリック
dblclick - ダブルクリック
mousedown/mouseup - マウスボタンを押す/離す
mouseover/mouseout - マウス要素上に入る/出る
keydown/keyup - キーを押す/離す
submit - フォーム送信
load - 読み込み完了
resize - サイズ変更
scroll - スクロール
*/

// イベント伝播の制御
document.getElementById("child").addEventListener("click", function(event) {
    event.stopPropagation();  // イベントの伝播を停止
});

// デフォルト動作の防止
document.getElementById("myLink").addEventListener("click", function(event) {
    event.preventDefault();  // リンクのデフォルト動作を防止
});
```

**使用事例:**

```javascript
// タブの切り替え機能
document.querySelectorAll(".tab").forEach(tab => {
    tab.addEventListener("click", function() {
        // アクティブクラスを全て削除
        document.querySelectorAll(".tab").forEach(t => {
            t.classList.remove("active");
        });
        
        // クリックされたタブをアクティブに
        this.classList.add("active");
        
        // コンテンツの表示切り替え
        const targetId = this.getAttribute("data-target");
        document.querySelectorAll(".content").forEach(content => {
            content.style.display = "none";
        });
        document.getElementById(targetId).style.display = "block";
    });
});

// ドラッグ＆ドロップ
const draggable = document.getElementById("draggable");
draggable.addEventListener("dragstart", function(event) {
    event.dataTransfer.setData("text/plain", this.id);
});

const dropZone = document.getElementById("dropZone");
dropZone.addEventListener("dragover", function(event) {
    event.preventDefault();  // ドロップを許可するために必要
});
dropZone.addEventListener("drop", function(event) {
    event.preventDefault();
    const draggedId = event.dataTransfer.getData("text/plain");
    const draggedElement = document.getElementById(draggedId);
    this.appendChild(draggedElement);
});
```

## 非同期処理

非同期操作を扱います。

```javascript
// コールバック関数
function fetchData(callback) {
    setTimeout(() => {
        const data = { name: "テストデータ" };
        callback(data);
    }, 1000);
}

fetchData(function(result) {
    console.log(result);  // { name: "テストデータ" }
});

// Promise
function fetchDataPromise() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const success = true;
            if (success) {
                resolve({ name: "テストデータ" });
            } else {
                reject("エラーが発生しました");
            }
        }, 1000);
    });
}

fetchDataPromise()
    .then(data => console.log(data))
    .catch(error => console.error(error));

// async/await
async function fetchDataAsync() {
    try {
        const response = await fetchDataPromise();
        console.log(response);
    } catch (error) {
        console.error(error);
    }
}

fetchDataAsync();

// fetch API
fetch("https://api.example.com/data")
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error("エラー:", error));
```

**使用事例:**

```javascript
// ユーザーデータを非同期で取得して表示
async function displayUserData(userId) {
    try {
        const response = await fetch(`https://api.example.com/users/${userId}`);
        
        if (!response.ok) {
            throw new Error("データの取得に失敗しました");
        }
        
        const userData = await response.json();
        
        // ユーザー情報を表示
        const userInfo = document.getElementById("userInfo");
        userInfo.innerHTML = `
            <h2>${userData.name}</h2>
            <p>メール: ${userData.email}</p>
            <p>電話: ${userData.phone}</p>
        `;
    } catch (error) {
        console.error("エラー:", error);
        document.getElementById("userInfo").innerHTML = 
            `<p class="error">ユーザー情報の取得に失敗しました</p>`;
    }
}

// ユーザーID 123のデータを表示
displayUserData(123);
```

## エラー処理

エラーを適切に処理します。

```javascript
// try...catch
try {
    // エラーが発生する可能性のあるコード
    const result = someUndefinedFunction();
} catch (error) {
    console.error("エラーが発生しました:", error.message);
} finally {
    // エラーの有無にかかわらず実行されるコード
    console.log("処理を完了しました");
}

// 特定のエラーの処理
try {
    throw new Error("カスタムエラー");
} catch (error) {
    if (error instanceof TypeError) {
        console.error("型エラー:", error.message);
    } else if (error instanceof ReferenceError) {
        console.error("参照エラー:", error.message);
    } else {
        console.error("その他のエラー:", error.message);
    }
}

// カスタムエラーの作成
class ValidationError extends Error {
    constructor(message) {
        super(message);
        this.name = "ValidationError";
    }
}

try {
    throw new ValidationError("入力値が無効です");
} catch (error) {
    console.error(`${error.name}: ${error.message}`);
}
```

**使用事例:**

```javascript
// フォームデータのバリデーション
function validateUserInput(username, password) {
    try {
        if (!username) {
            throw new ValidationError("ユーザー名は必須です");
        }
        
        if (password.length < 8) {
            throw new ValidationError("パスワードは8文字以上必要です");
        }
        
        return true;  // バリデーション成功
    } catch (error) {
        if (error instanceof ValidationError) {
            // バリデーションエラーの処理
            document.getElementById("errorMessage").textContent = error.message;
        } else {
            // その他の予期しないエラーの処理
            console.error("システムエラー:", error);
            document.getElementById("errorMessage").textContent = 
                "システムエラーが発生しました。後でもう一度お試しください。";
        }
        return false;  // バリデーション失敗
    }
}

// フォーム送信時の処理
document.getElementById("loginForm").addEventListener("submit", function(event) {
    const username = document.getElementById("username").value;
    const password = document.getElementById("password").value;
    
    if (!validateUserInput(username, password)) {
        event.preventDefault();  // バリデーション失敗時はフォーム送信を中止
    }
});
```