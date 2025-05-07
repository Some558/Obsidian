Markdownは軽量マークアップ言語で、シンプルな記法でテキストを構造化できます。以下に基本的な文法をまとめました。

## 見出し

markdown

```markdown
# 見出し1
## 見出し2
### 見出し3
#### 見出し4
##### 見出し5
###### 見出し6
```

## テキスト装飾

markdown

```markdown
*斜体* または _斜体_
**太字** または __太字__
***太字と斜体*** または ___太字と斜体___
~~取り消し線~~
```

## リスト

### 番号なしリスト

markdown

```markdown
- 項目1
- 項目2
  - ネストした項目
  - ネストした項目
- 項目3
```

### 番号付きリスト

markdown

```markdown
1. 項目1
2. 項目2
   3. ネストした項目
   4. ネストした項目
5. 項目3
```

## リンク

markdown

```markdown
[リンクテキスト](URL "タイトル(省略可)")
[Google](https://www.google.com "Googleへ")
```

## 画像

markdown

```markdown
![代替テキスト](画像URL "タイトル(省略可)")
![ロゴ](logo.png "ロゴ")
```

## 引用

markdown

```markdown
> これは引用文です
> 
> > ネストした引用
```

## コード

### インラインコード

markdown

```markdown
`インラインコード`
```

### コードブロック

markdown

````markdown
```言語名(省略可)
コードブロック
複数行にわたるコード
```
````

## 水平線

markdown

```markdown
---
***
___
```

## テーブル

markdown

```markdown
| 見出し1 | 見出し2 | 見出し3 |
|--------|--------|--------|
| セル1   | セル2   | セル3   |
| セル4   | セル5   | セル6   |
```

## チェックボックス

markdown

```markdown
- [ ] 未完了タスク
- [x] 完了タスク
```

## エスケープ文字

markdown

```markdown
\*エスケープされたアスタリスク\*
```

## 脚注

markdown

```markdown
脚注の例[^1]です。

[^1]: これは脚注の内容です。
```

## HTMLタグ

markdown

```markdown
Markdownでは一部の<b>HTMLタグ</b>も使用できます。
```