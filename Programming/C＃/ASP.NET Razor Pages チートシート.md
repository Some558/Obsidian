

## 基本的なディレクティブ

csharp

```csharp
@page                       // Razor Pageであることを宣言
@model LoginModel           // モデルの指定
@using Microsoft.AspNetCore.Mvc // 名前空間のインポート
@inject IService Service    // サービスの注入
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers // TagHelperの追加
```

## フォーム関連のタグヘルパー

html

```html
<form method="post">
    <!-- 入力フィールド -->
    <div>
        <label asp-for="Customer.Name"></label>
        <input asp-for="Customer.Name" />
        <span asp-validation-for="Customer.Name"></span>
    </div>
    
    <!-- ドロップダウンリスト -->
    <select asp-for="Customer.CountryId" asp-items="Model.Countries"></select>
    
    <!-- チェックボックス -->
    <input type="checkbox" asp-for="Customer.IsSubscribed" />
    
    <!-- ラジオボタン -->
    <input type="radio" asp-for="Customer.Gender" value="M" /> 男性
    <input type="radio" asp-for="Customer.Gender" value="F" /> 女性
    
    <!-- 送信ボタン -->
    <button type="submit">保存</button>
</form>
```

## バリデーション

html

```html
<div asp-validation-summary="All"></div>     <!-- すべてのバリデーションエラー -->
<div asp-validation-summary="ModelOnly"></div> <!-- フィールドに関連しないエラー -->
<span asp-validation-for="Customer.Email"></span> <!-- 特定フィールドのエラー -->
```

## リンク関連のタグヘルパー

html

```html
<!-- ページへのリンク -->
<a asp-page="/Products/Details" asp-route-id="@product.Id">詳細</a>

<!-- 同じフォルダ内のページへのリンク -->
<a asp-page="./Edit" asp-route-id="@item.Id">編集</a>

<!-- エリアを指定したリンク -->
<a asp-page="/Index" asp-area="Admin">管理画面</a>

<!-- ページハンドラーへのリンク -->
<a asp-page-handler="Delete" asp-route-id="@item.Id">削除</a>
```

## 部分ビュー

csharp

```csharp
@await Html.PartialAsync("_PartialName", Model)
// または
<partial name="_PartialName" model="@Model" />
```

## ループと条件分岐

csharp

```csharp
@foreach (var item in Model.Items)
{
    <p>@item.Name</p>
}

@if (Model.IsAdmin)
{
    <p>管理者向けコンテンツ</p>
}
else
{
    <p>一般ユーザー向けコンテンツ</p>
}

@switch (Model.UserType)
{
    case UserType.Admin:
        <p>管理者</p>
        break;
    case UserType.Customer:
        <p>顧客</p>
        break;
}
```

## レイアウト

csharp

```csharp
@{
    Layout = "_Layout";  // レイアウトの指定
    ViewData["Title"] = "ページタイトル";
}
```

## セクション

csharp

```csharp
@section Scripts {
    <script src="~/js/myscript.js"></script>
}
```

## アンチフォージェリートークン

html

```html
@Html.AntiForgeryToken()
// または
<form asp-antiforgery="true">...</form>
```

## 画像とスクリプト

html

```html
<img asp-append-version="true" src="~/images/logo.png" />
<script asp-append-version="true" src="~/js/site.js"></script>
```

## 環境による条件分岐

csharp

```csharp
<environment include="Development">
    <link rel="stylesheet" href="~/css/site.css" />
</environment>
<environment exclude="Development">
    <link rel="stylesheet" href="~/css/site.min.css" asp-append-version="true" />
</environment>
```

## タグヘルパーの属性一覧

|タグヘルパー属性|説明|
|---|---|
|asp-for|モデルのプロパティにバインド|
|asp-items|セレクトリストのオプションを生成|
|asp-validation-for|特定フィールドの検証メッセージを表示|
|asp-validation-summary|検証エラーのサマリーを表示|
|asp-page|リンク先のRazorページを指定|
|asp-page-handler|ページハンドラーを指定|
|asp-route-{value}|ルートパラメータを指定|
|asp-area|エリアを指定|
|asp-antiforgery|アンチフォージェリートークンを含めるかどうか|
|asp-append-version|ファイルにバージョンを付与|

## ページモデルでのハンドラーメソッド例

csharp

```csharp
public class IndexModel : PageModel
{
    // GETリクエスト
    public async Task OnGetAsync()
    {
        // 処理
    }
    
    // POSTリクエスト
    public async Task<IActionResult> OnPostAsync()
    {
        if (!ModelState.IsValid)
        {
            return Page();
        }
        
        // 処理
        return RedirectToPage("./Index");
    }
    
    // カスタムハンドラー
    public async Task<IActionResult> OnPostDeleteAsync(int id)
    {
        // 削除処理
        return RedirectToPage();
    }
}
```

## TempDataとViewData

csharp

```csharp
// コントローラーまたはPageModel内
TempData["Message"] = "成功しました";
ViewData["Title"] = "ページタイトル";

// Razor View内で使用
<p>@TempData["Message"]</p>
<h1>@ViewData["Title"]</h1>
```