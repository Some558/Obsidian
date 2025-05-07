

Package Manager Console（PMC）を使用したEntity Frameworkのマイグレーションコマンドのチートシートです。これらのコマンドは Visual Studio の「ツール」→「NuGet パッケージマネージャー」→「パッケージマネージャーコンソール」から実行します。

## 前提条件パッケージ

```
Install-Package Microsoft.EntityFrameworkCore.Tools
Install-Package Microsoft.EntityFrameworkCore.Design
```

## 基本的なマイグレーションコマンド

powershell

```powershell
# マイグレーションの追加
Add-Migration InitialCreate

# 特定のDbContextを指定
Add-Migration InitialCreate -Context ApplicationDbContext

# 出力ディレクトリの指定
Add-Migration InitialCreate -OutputDir Data/Migrations

# プロジェクトの指定
Add-Migration InitialCreate -Project MyProject.Data

# スタートアッププロジェクトの指定
Add-Migration InitialCreate -StartupProject MyProject.Web

# マイグレーションの削除
Remove-Migration

# 直前のマイグレーションをロールバック（まだ適用されていない場合）
Remove-Migration -Force
```

## データベース更新コマンド

powershell

```powershell
# データベースを最新のマイグレーションまで更新
Update-Database

# 特定のマイグレーションまで更新
Update-Database -Migration AddProductTable

# 最初の状態に戻す（すべてのマイグレーションをロールバック）
Update-Database -Migration 0

# 特定のDbContextを指定
Update-Database -Context ApplicationDbContext

# 接続文字列を指定
Update-Database -Connection "Server=(localdb)\mssqllocaldb;Database=MyDatabase;Trusted_Connection=True;"
```

## マイグレーションスクリプト生成

powershell

```powershell
# マイグレーションスクリプトの生成
Script-Migration

# 特定の範囲のマイグレーションスクリプトを生成
Script-Migration InitialCreate AddProductTable

# 特定のマイグレーションから最新までのスクリプトを生成
Script-Migration AddCustomerTable

# 最初から特定のマイグレーションまでのスクリプトを生成
Script-Migration -To AddProductTable

# スクリプトの出力先を指定
Script-Migration -Output "C:\Migrations\script.sql"

# 冪等性スクリプトの生成（何度実行しても同じ結果になる）
Script-Migration -Idempotent
```

## マイグレーション情報の取得

powershell

```powershell
# すべてのマイグレーションの一覧表示
Get-Migration

# 特定のDbContextのマイグレーション一覧
Get-Migration -Context ApplicationDbContext

# DbContextの情報表示
Get-DbContext

# スキャフォールディング（リバースエンジニアリング）
Scaffold-DbContext "Server=myserver;Database=mydb;User Id=myuser;Password=mypass;" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models

# 特定のテーブルのみスキャフォールディング
Scaffold-DbContext "Connection String" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models -Tables Customers, Orders

# 既存のDbContextを上書き
Scaffold-DbContext "Connection String" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models -Context MyDbContext -Force
```

## コンテキスト操作

powershell

```powershell
# DbContextの一覧表示
Get-DbContext

# 特定のプロジェクトのDbContext一覧
Get-DbContext -Project MyProject.Data
```

## オプションフラグ

powershell

```powershell
# 詳細なログ出力を有効化
Add-Migration InitialCreate -Verbose

# ドライラン（実際には変更を適用しない）
Update-Database -WhatIf
```

## 一般的なワークフロー例

powershell

```powershell
# 1. モデルを作成/変更した後、マイグレーションを追加
Add-Migration AddProductTable

# 2. 生成されたマイグレーションファイルを確認/編集
# (マイグレーションファイルは通常 Migrations フォルダにあります)

# 3. データベースを更新
Update-Database

# または、本番環境用にスクリプトを生成
Script-Migration -Idempotent -Output "update_script.sql"
```

## 特定の環境用コマンド

powershell

```powershell
# 開発環境用
Update-Database -Environment Development

# 本番環境用
Update-Database -Environment Production
```

## エラー対処

powershell

```powershell
# マイグレーションのリセット（データベースを削除して再作成）
Drop-Database

# 強制的にマイグレーションを削除（注意: 未適用のマイグレーションのみ）
Remove-Migration -Force
```