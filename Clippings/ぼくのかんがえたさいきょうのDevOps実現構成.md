---
title: "ぼくのかんがえたさいきょうのDevOps実現構成"
source: "https://zenn.dev/istone/articles/297833b006dfd6"
author:
  - "[[Zenn]]"
published: 2024-03-04
created: 2025-06-03
description:
tags:
  - "clippings"
---
223

7[tech](https://zenn.dev/tech-or-idea)

## はじめに

昨年、AWS のインフラを運用・監視する上で使いやすいと思ったサービスを組み合わせて構成図を紹介した記事、「 **[【AWS】ぼくのかんがえたさいきょうの運用・監視構成](https://qiita.com/iStone/items/72417fe599e71e62f631)** 」が投稿したその日の Qiita のトレンド 1 位になり、はてなブックマークのテクノロジー分野でトップを飾りました。（たくさんの方に見ていただき感謝してます！）

本記事では「 **ぼくのかんがえたさいきょうの運用・監視構成** 」の続編として「 **ぼくのかんがえたさいきょうの DevOps 実現構成** 」を紹介させていただきます。あくまでも「ぼくのかんがえた」なので私個人の意見として受け入れていただけると助かります。

前回の記事でもお伝えいたしましたが、各個人・企業によって環境は違うと思いますし、使いやすいサービスは人それぞれだと思うので、これが正解という訳ではありません。一個人の意見として参考にしてただければ幸いです。

また、こちらの記事は 2024 年 3 月時点での情報です。料金改定により、コストパフォーマンス悪くなったり、新たに便利なサービスが登場する可能性もあります。

## 全体図

こちらが「 **ぼくのかんがえたさいきょうの DevOps 実現構成** 」の全体図です。簡単に説明すると「 **GitHub + α** 」⇄「 **Grafana Cloud + α** 」で **Dev** ⇄ **Ops** のループを回す構成を表しています。

[![](https://res.cloudinary.com/zenn/image/fetch/s--x1IyUiZt--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_1200/https://images.microcms-assets.io/assets/0402567430be43b4a7db9f7365e62718/7f2db45ddd184d5389f0d1f3a1874c6c/devops.drawio.png)](https://images.microcms-assets.io/assets/0402567430be43b4a7db9f7365e62718/7f2db45ddd184d5389f0d1f3a1874c6c/devops.drawio.png)

※クリックで拡大

できるだけ費用を抑え、かつ便利な SaaS を選択しました。今回は DevOps を実現する構成として様々なツールを紹介しますが、あくまでもツールは DevOps の手段であって、ツールの導入だけでは DevOps を実現できません。

まずは DevOps について解説していきます。

## DevOps とは

DevOps とは、ソフトウェアの開発（Dev）と運用（Ops）の壁を取り除いてフレキシブルかつスピーディーに開発することで、システムの継続的な向上・改善を目指す文化や技術、プロセスのことを指します。

![](https://storage.googleapis.com/zenn-user-upload/de02d017545e-20240227.png)

DevOps が実現できていると、 **Plan** → **Code** → **Build** → **Release** → **Deploy** → **Operate** → **Monitor** のプロセスを繰り返して、システムの向上・改善を素早く行うことができます。

これだけでは DevOps に具体的にイメージしづらい思うので、DevOps の指標をいくつか紹介します。それぞれ共通する部分が多いのでイメージしやすいのではないでしょうか。

## DevOps と「CALMS」

組織が DevOps を導入する能力を評価するためのフレームワークとして「CALMS」と呼ばれるものがあり、下記の 5 つの頭文字から名付けられています。

### Culture（文化）

組織文化の変革を促す。

### Automation（自動化）

手作業のプロセスを自動化して速度と信頼性を向上させる。

### Lean（無駄がない）

開発フローを改善して無駄を削減し、価値の提供を最大化する。

### Measurement（計測）

パフォーマンス指標やフィードバックループを活用して、継続的な改善を促進する。

### Sharing（共有）

知識や情報を共有する。

## DevOps の「3 つの道」

「 [The DevOps 　逆転だ！究極の継続的デリバリー](https://amzn.asia/d/7zvMDaT) 」や「 [The DevOps ハンドブック 理論・原則・実践のすべて](https://amzn.asia/d/7UUYl86) 」では DevOps の行動原理はすべてこの 3 つから導き出せるとして、下記の 3 つを挙げています。

### フローの原則

開発 → 運用 → 顧客のワークフローを高速にする。

### フィードバックの原則

すばやくてコンスタントなフィードバックフローを実現する。

### 継続的な学習と実験の原則

成功と失敗の両方から組織として学習し教訓を得ていく文化を育む。

## DevOps の「4 本柱」

「 [Effective DevOps](https://www.oreilly.co.jp/books/9784873118352/) 」では効果的な DevOps のための 4 本柱として下記の 4 つを挙げています。

### コラボレーション

チーム間の壁を取り除き、オープンなコミュニケーションと協力を促進する。

### アフィニティ

共通の目的やゴールに向かってチームが一丸となる。

### ツール

適切なツールを選定して利用する。

### スケーリング

DevOps 文化を組織全体に拡大する。

## DevOps の「Four Keys」

[DevOps Research and Assessment（DORA）](https://dora.dev/) チームは、6 年間の研究を基に、ソフトウェア開発チームのパフォーマンスを示す 4 つの指標として下記の 4 つを挙げています。「 [Lean と DevOps の科学](https://amzn.asia/d/2sEB6hC) 」という書籍でも紹介されています。

### デプロイの頻度

正常な本番環境へのリリースの頻度。

### 変更のリードタイム

commit から本番環境稼働までの所要時間。

### 平均復旧時間

本番環境での障害から回復するのにかかる時間。

### 変更失敗率

デプロイが原因で本番環境にて障害が発生する割合。  
  
2017 年時点で、パフォーマンスが低い組織と比較して、パフォーマンスが良好な組織は次のとおりになったそうです。

- デプロイの頻度が 46 倍（1 日複数回）
- 変更のリードタイムが 1/440（1 時間未満）
- 平均復旧時間は 1/170（1 時間未満）
- 変更失敗率は 1/5（0-15％）

## DevOps の能力（ケイパビリティ）

また [DevOps Research and Assessment（DORA）](https://dora.dev/) チームは他にも、ソフトウェア デリバリーと組織のパフォーマンスを改善するための能力を調査・検証し、DevOps のケイパビリティとして公開しています。

DevOps のケイパビリティは **技術に関するケイパビリティ** ・ **プロセスに関するケイパビリティ** ・ **文化に関するケイパビリティ** の 3 つに分類されており、全部で 27 のケイパビリティが紹介されています。「 [Lean と DevOps の科学](https://amzn.asia/d/2sEB6hC) 」という書籍でも紹介されていますが、こちらの書籍の発売時（2018 年）は 24 個でした。

### 技術に関するケイパビリティ

- [クラウドインフラストラクチャ](https://cloud.google.com/architecture/devops/devops-tech-cloud-infrastructure?hl=ja)
- [コードの保守性](https://cloud.google.com/architecture/devops/devops-tech-code-maintainability?hl=ja)
- [継続的デリバリー](https://cloud.google.com/architecture/devops/devops-tech-continuous-delivery?hl=ja)
- [継続的インテグレーション](https://cloud.google.com/architecture/devops/devops-tech-continuous-integration?hl=ja)
- [継続的なテスト](https://cloud.google.com/architecture/devops/devops-tech-test-automation?hl=ja)
- [データベースのチェンジマネジメント](https://cloud.google.com/architecture/devops/devops-tech-database-change-management?hl=ja)
- [デプロイの自動化](https://cloud.google.com/architecture/framework/operational-excellence/automate-your-deployments?hl=ja)
- [チームのツール選択をサポート](https://cloud.google.com/architecture/devops/devops-tech-teams-empowered-to-choose-tools?hl=ja)
- [疎結合アーキテクチャ](https://cloud.google.com/architecture/devops/devops-tech-architecture?hl=ja)
- [モニタリングとオブザーバビリティ](https://cloud.google.com/architecture/devops/devops-measurement-monitoring-and-observability?hl=ja)
- [セキュリティのシフトレフト](https://cloud.google.com/architecture/devops/devops-tech-shifting-left-on-security?hl=ja)
- [テストデータ管理](https://cloud.google.com/architecture/devops/devops-tech-test-data-management?hl=ja)
- [トランクベース開発](https://cloud.google.com/architecture/devops/devops-tech-trunk-based-development?hl=ja)
- [バージョン管理](https://cloud.google.com/architecture/devops/devops-tech-version-control?hl=ja)

### プロセスに関するケイパビリティ

- [顧客からのフィードバック](https://cloud.google.com/architecture/devops/devops-process-customer-feedback?hl=ja)
- [システムをモニタリングして的確な判断](https://cloud.google.com/architecture/devops/devops-measurement-monitoring-systems?hl=ja)
- [障害の予兆通知](https://cloud.google.com/architecture/devops/devops-measurement-proactive-failure-notification?hl=ja)
- [変更承認の効率化](https://cloud.google.com/architecture/devops/devops-process-streamlining-change-approval?hl=ja)
- [チームのテスト](https://cloud.google.com/architecture/devops/devops-process-team-experimentation?hl=ja)
- [バリューストリームでの作業の可視性](https://cloud.google.com/architecture/devops/devops-process-work-visibility-in-value-stream?hl=ja)
- [ビジュアル管理機能](https://cloud.google.com/architecture/devops/devops-measurement-visual-management?hl=ja)
- [仕掛り制限](https://cloud.google.com/architecture/devops/devops-measurement-wip-limits?hl=ja)
- [小さいバッチ単位の作業](https://cloud.google.com/architecture/devops/devops-process-working-in-small-batches?hl=ja)

### 文化に関するケイパビリティ

- [創造的な組織文化](https://cloud.google.com/architecture/devops/devops-culture-westrum-organizational-culture?hl=ja)
- [仕事の満足度](https://cloud.google.com/architecture/devops/devops-culture-job-satisfaction?hl=ja)
- [学習文化](https://cloud.google.com/architecture/devops/devops-culture-learning-culture?hl=ja)
- [変革型リーダーシップ](https://cloud.google.com/architecture/devops/devops-culture-transformational-leadership?hl=ja)

## DevOps のアンチパターン

「 [Effective DevOps](https://www.oreilly.co.jp/books/9784873118352/) 」には DevOps のアンチパターンとして下記の 4 つが紹介されています。

### 非難文化

エラーやインシデントの原因を作った人を非難し処罰する。

### サイロ

同じ企業の他のチームと知識を共有しない。

### 根本原因分析

直接の原因ばかりが注目されて、間接的に影響を与えたかもしれない要素が目に入らなくなる。

### ヒューマンエラー

ミスを犯した人がエラーの直接的な原因にする。

また、オライリーの「 [システム運用アンチパターン](https://www.oreilly.co.jp//books/9784873119847/) 」にて、

> 本書は、一般のエンジニアやチームリーダーが DevOps による変革を起こすための手助けになるよう書かれたものです。

との記載があるので、こちらの書籍で紹介されているアンチパターンも紹介します。

### パターナリスト症候群

仕事の進め方やタイミングを権力の持つ人に委ねる。

### 盲目状態での運用

システムが期待通りの処理が行われているかどうか確認するためのツールを使用せず運用する。

### 情報ではなくデータ

利用者を考えたダッシュボード作成をしていない。

### 最後の味付けとしての品質

意味のないテストを行なっている。

### アラート疲れ

ノイズになっているアラートが多すぎて重要なアラートに気付けない。

### 空の道具箱

運用が自動化されていない。

### 業務時間外のデプロイ

業務時間外にデプロイする。

### せっかくのインシデントを無駄にする

インシデントを今後の改善に活かさない。

### 情報のため込み

情報を共有しない。

### 命じられた文化

組織の文化が形骸化している。

### 多すぎる尺度

作業の優先順位づけがされていない。

## DevOps は”文化”

オライリーの「 [ソフトウェアアーキテクチャメトリクス](https://www.oreilly.co.jp/books/9784814400607/) 」では、

> DevOps の主要な焦点は **文化** であり、ツールや自動化はそれに続くものと言えます。

とあります。

また、「 [Effective DevOps](https://www.oreilly.co.jp/books/9784873118352/) 」にも、

> devops は文化運動である。あなたの環境において今使っているツールは、あなたの文化の一部である。

> ツールは、現在の組織文化と方向性にもとづいて、改革を支え加速していく存在である。

とあります。

今回はツールの紹介となりますが、ツールの導入で満足するのではなく、ツールを通じて DevOps の **文化** を育むことが重要となります。

## 料金

今回紹介する SaaS の料金です。変動があるかと思うので公式サイトの料金ページの紹介に留めます。

- [Grafana Cloud](https://grafana.com/pricing/)
- [GitHub Actions](https://docs.github.com/ja/billing/managing-billing-for-github-actions/about-billing-for-github-actions)
- [Snyk](https://snyk.io/jp/plans/)
- [CodeRabbit](https://docs.coderabbit.ai/about/pricing/)
- [Qase](https://qase.io/pricing)
- [Checkly](https://www.checklyhq.com/pricing/)
- [Sentry](https://sentry.io/pricing/)
- [LaunchDarkly](https://launchdarkly.com/pricing/)

それでは本構成について紹介していきます。

## GitHub でソースコード管理

ソースコード管理は GitHub で行います。「 [DevOps のケイパビリティ](https://zenn.dev/istone/articles/#devops-%E3%81%AE%E8%83%BD%E5%8A%9B%EF%BC%88%E3%82%B1%E3%82%A4%E3%83%91%E3%83%93%E3%83%AA%E3%83%86%E3%82%A3%EF%BC%89) 」における **バージョン管理** に関するケイパビリティをサポートします。

## GitHub

**GitHub** は Git を利用してコードの保存と公開が出来、他の開発者と一緒にコードのレビューをしたり、プロジェクトを管理しながら、ソフトウェアの開発できるサービスです。

### コードの保守性 & 疎結合アーキテクチャ

「 [DevOps のケイパビリティ](https://zenn.dev/istone/articles/#devops-%E3%81%AE%E8%83%BD%E5%8A%9B%EF%BC%88%E3%82%B1%E3%82%A4%E3%83%91%E3%83%93%E3%83%AA%E3%83%86%E3%82%A3%EF%BC%89) 」には **コードの保守性** が紹介されていました。Google では、「DevOps のケイパビリティ」の 1 つである **トランクベース開発** や、全てのコードを 1 つのリポジトリに集約する **モノリシックリポジトリ** を採用することで、コードの保守性を向上しているようです。

また、「 [DevOps のケイパビリティ](https://zenn.dev/istone/articles/#devops-%E3%81%AE%E8%83%BD%E5%8A%9B%EF%BC%88%E3%82%B1%E3%82%A4%E3%83%91%E3%83%93%E3%83%AA%E3%83%86%E3%82%A3%EF%BC%89) 」には **疎結合アーキテクチャ** についても紹介されていました。「 **テスト容易性** 」と「 **デプロイ容易性** 」がパフォーマンスの向上に重要であり、この 2 つの特性を持たせるには、システムは疎結合である必要があると「 [Lean と DevOps の科学](https://amzn.asia/d/2sEB6hC) 」に記載されています。  
**マイクロサービスアーキテクチャ** の採用や、マイクロサービスの境界を明確にするための **ドメイン駆動設計** (**DDD**)の採用が考えられます。

### GitHub のデータを Grafana で可視化

Grafana には GitHub をデータソースとして利用できるプラグインが用意されており、GitHub のデータを可視化できます。

「 [DevOps のケイパビリティ](https://zenn.dev/istone/articles/#devops-%E3%81%AE%E8%83%BD%E5%8A%9B%EF%BC%88%E3%82%B1%E3%82%A4%E3%83%91%E3%83%93%E3%83%AA%E3%83%86%E3%82%A3%EF%BC%89) 」における **バリューストリームでの作業の可視性** に寄与し、「 [Four Keys](https://zenn.dev/istone/articles/#devops-%E3%81%AE%E3%80%8Cfour-keys%E3%80%8D) 」の 4 つの指標のうち、 **変更のリードタイム** を把握しやすくなります。

### SDK の導入

そして、今回の構成を実現するためにはアプリケーションに下記 4 つの SDK を導入する必要があります。

- [**OpenTelemetry SDK**](https://zenn.dev/istone/articles/#opentelemetry-sdk)
- [**Pyroscope SDK**](https://zenn.dev/istone/articles/#pyroscope-sdk)
- [**Sentry SDK**](https://zenn.dev/istone/articles/#sentry-sdk)
- [**OpenFeature SDK**](https://zenn.dev/istone/articles/#openfeature-sdk)

それぞれの SDK について紹介していきます。

## OpenTelemetry SDK

**OpenTelemetry** はメトリクス・ログ・トレースなどのアプリケーションを監視するためのデータの収集を標準化するための CNCF のプロジェクトです。このプロジェクトの SDK を使用してアプリケーションのトレースデータを取得します。

トレースとは、メトリクスやログなどと同じくアプリケーションを監視するためのデータの 1 つで、メトリクス・ログ・トレースを３つ合わせてオブザーバビリティの 3 本柱と言われており、複数のサーバーを伝播する特定のリクエストの追跡データを取得します。

後述する [**Grafana Tempo**](https://zenn.dev/istone/articles/#%E3%83%88%E3%83%AC%E3%83%BC%E3%82%B9\(grafana-tempo\)) はこの **OpenTelemetry** に対応しているので、この **OpenTelemetry** の SDK から **Grafana Tempo** にトレースデータを送信します。

![](https://storage.googleapis.com/zenn-user-upload/d256f1c343f5-20240227.png)

### CNCF

CNCF(Cloud Native Computing Foundation) とは Linux Foundation のプロジェクトの 1 つで、クラウドネイティブなコンピューティングシステムを推進するための非営利団体の事です。今回の構成では CFCF のプロジェクトとして、他にも [**OpenFeature**](https://zenn.dev/istone/articles/#openfeature-sdk) や [**Prometheus**](https://zenn.dev/istone/articles/#%E3%83%A1%E3%83%88%E3%83%AA%E3%82%AF%E3%82%B9\(prometheus\)) を紹介します。

## Pyroscope SDK

**Pyroscope** は継続的プロファイリングを行うためのツールで、この SDK を使用してアプリケーションの継続的プロファイリングを行います。

継続的プロファイリングとは先ほどのオブザーバビリティの 3 本柱に次ぐ 4 本目の柱とも言われており、アプリケーションのどのコードがどの程度の CPU やメモリを消費しているか、実行時間がどのくらいかかっているかを把握するためのデータを取得します。

後述する [**Grafana Pyroscope**](https://zenn.dev/istone/articles/#%E7%B6%99%E7%B6%9A%E7%9A%84%E3%83%97%E3%83%AD%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AA%E3%83%B3%E3%82%B0\(grafana-pyroscope\)) にプロファイリングデータを送信します。

![](https://storage.googleapis.com/zenn-user-upload/f2ad034b21dd-20240227.png)

## Sentry SDK

**Sentry** は RUM (Real User Monitoring)やエラートラッキングを行うためのツールで、この SDK を使用してアプリケーションのエラートラッキングを行います。

RUM とはリアルユーザーの視点からアプリケーションのフロントエンドパフォーマンスを監視することです。また、エラートラッキングとはアプリケーションのエラーを監視することです。ログとの違いについては [こちら](https://sentry.io/vs/logging/) をご覧ください。

後述する [**Sentry**](https://zenn.dev/istone/articles/#%E3%82%A8%E3%83%A9%E3%83%BC%E3%83%88%E3%83%A9%E3%83%83%E3%82%AD%E3%83%B3%E3%82%B0\(sentry\)) にエラートラッキングしたデータを送信します。

![](https://storage.googleapis.com/zenn-user-upload/384bf453dd91-20240227.png)

### TEMPLE

**OpenTelemetry** や **Jaeger** を作った人が提唱した概念で、オブザーバビリティの 4 つの柱に `Event` と `Exception` を加えた 6 つの柱のことで、下記記事に詳しく書かれています。  
記事でも紹介されている通り、Sentry は `Exception` にあたります。

## OpenFeature SDK

**OpenFeature** はフィーチャーフラグの管理を標準化するための CNCF プロジェクトで、これに順守しているサービスであれば共通の SDK を使用してフィーチャーフラグを管理できます。

フィーチャーフラグは、コードを直接変更せずに、特定の機能をオンまたはオフにできる技術です。これにより、新機能を特定のユーザーのみに表示したり、AB テストなどの機能テストを行うことが可能です。「 [DevOps のケイパビリティ](https://zenn.dev/istone/articles/#devops-%E3%81%AE%E8%83%BD%E5%8A%9B%EF%BC%88%E3%82%B1%E3%82%A4%E3%83%91%E3%83%93%E3%83%AA%E3%83%86%E3%82%A3%EF%BC%89) 」における **小さいバッチ単位の作業** においてもフィーチャーフラグの使用が紹介されています。

後述する [**LaunchDarkly**](https://zenn.dev/istone/articles/#%E3%83%95%E3%82%A3%E3%83%BC%E3%83%81%E3%83%A3%E3%83%BC%E3%83%95%E3%83%A9%E3%82%B0\(launchdarkly\)) はこの **OpenFeature** に対応しているので、 **LaunchDarkly** を使用してでフィーチャーフラグを管理します。

![](https://storage.googleapis.com/zenn-user-upload/a910bbea350f-20240227.png)

## GitHub Actions で CI/CD を実装

**GitHub Actions** を用いて、継続的インテグレーション/継続的デリバリー（CI/CD）を行います。「 [DevOps のケイパビリティ](https://zenn.dev/istone/articles/#devops-%E3%81%AE%E8%83%BD%E5%8A%9B%EF%BC%88%E3%82%B1%E3%82%A4%E3%83%91%E3%83%93%E3%83%AA%E3%83%86%E3%82%A3%EF%BC%89) 」における **継続的デリバリー・継続的インテグレーション・継続的なテスト・デプロイの自動化** といったケイパビリティをサポートします。

## GitHub Actions

GitHub Actions は、ビルド、テスト、デプロイのパイプラインを自動化できる CI/CD サービスです。

今回の構成の CI/CD では下記の 5 つのステップを採用しました。

- [フォーマット＆静的解析](https://zenn.dev/istone/articles/#%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%83%E3%83%88-%26-%E9%9D%99%E7%9A%84%E8%A7%A3%E6%9E%90\(biome%2C-etc.\))
- [単体テスト＆結合テスト](https://zenn.dev/istone/articles/#%E5%8D%98%E4%BD%93%E3%83%86%E3%82%B9%E3%83%88-%26-%E7%B5%90%E5%90%88%E3%83%86%E3%82%B9%E3%83%88\(vitest%2C-etc.\))
- [ビルド](https://zenn.dev/istone/articles/#%E3%83%93%E3%83%AB%E3%83%89\(vite%2C-etc.\))
- [アプリケーションのデプロイ](https://zenn.dev/istone/articles/#%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E3%83%87%E3%83%97%E3%83%AD%E3%82%A4\(docker\))
- [インフラのプロビジョニング](https://zenn.dev/istone/articles/#%E3%82%A4%E3%83%B3%E3%83%95%E3%83%A9%E3%81%AE%E3%83%97%E3%83%AD%E3%83%93%E3%82%B8%E3%83%A7%E3%83%8B%E3%83%B3%E3%82%B0\(terraform\))

![](https://storage.googleapis.com/zenn-user-upload/b957e04b0117-20240229.png)

ここでは含めませんでしたが、後述する下記３つも GitHub Actions 上で実行可能です。

- [セキュリティスキャン](https://zenn.dev/istone/articles/#%E3%82%BB%E3%82%AD%E3%83%A5%E3%83%AA%E3%83%86%E3%82%A3%E3%82%B9%E3%82%AD%E3%83%A3%E3%83%B3\(snyk\))
- [E2E テスト](https://zenn.dev/istone/articles/#%E5%A4%96%E5%BD%A2%E7%9B%A3%E8%A6%96%E3%81%A8-e2e-%E3%83%86%E3%82%B9%E3%83%88\(checkly\))
- [負荷テスト](https://zenn.dev/istone/articles/#%E8%B2%A0%E8%8D%B7%E3%83%86%E3%82%B9%E3%83%88\(grafana-k6\))

![](https://storage.googleapis.com/zenn-user-upload/407ff38f69bd-20240229.png)

### GitHub Actions のログを Grafana Loki に送信

**GitHub Actions** のログを **Grafana Loki** に送信することで、ワークフローの実行時間やエラーの発生箇所を可視化できます。  
また、メトリクスやアプリケーションログのデータと連携することで、デプロイによる影響も把握しやすくなります。

「 [Four Keys](https://zenn.dev/istone/articles/#devops-%E3%81%AE%E3%80%8Cfour-keys%E3%80%8D) 」の 4 つの指標のうち、 **デプロイの頻度** や **変更失敗率** を把握するためにも有用です。

こちらを実行するための GitHub Actions のアクションを作成したので、是非ご活用ください。

## フォーマット & 静的解析(Biome, etc.)

フォーマットはソースコードを整形することで、静的解析は文法上の誤りやバグの原因となるようなコードを解析することです。

JavaScript だとフォーマットには [**Prettier**](https://prettier.io/) 、静的解析には [**ESlint**](https://eslint.org/) が有名で、フォーマットと静的解析の両方が行えて、Prettier と ESLint との高い互換性のある [**Biome**](https://biomejs.dev/ja/) といったツールも注目を浴びています。  
その他、Go 言語では標準でフォーマットや静的解析の機能が用意されていたり、Terraform では標準でのフォーマットと [**TFLint**](https://github.com/terraform-linters/tflint) という静的解析ツールが用意されていたりします。

今回の構成では **Biome** を記載していますが、要件や言語によってその他のツールも考えられます。

## 単体テスト & 結合テスト(Vitest, etc.)

単体テストは関数やクラスが正しく機能するかをチェックするテストのことです。

JavaScript だと [**Jest**](https://jestjs.io/ja/) が有名で、 Jest と高い互換性があり Jest よりも高速な [**Vitest**](https://vitest.dev/) といったツールも注目を浴びています。Go 言語では標準でテストの機能が用意されていたりします。

また、結合テストは複数の関数やクラスを組み合わせて、それらが連携して正しく動くかを検証するテストのことです。

JavaScript だと [**Testing Library**](https://testing-library.com/) といったツールが有名です。

この **Testing Library** ですが、「Testing Trophy」というテストの考え方を提唱しており、「結合テスト」に最も比重を置くべきだとしています。

![](https://storage.googleapis.com/zenn-user-upload/bdec2fd20a8d-20240302.png)

※Static が静的解析、Unit が単体テスト、Integration が結合テスト、E2E が E2E テストを表しています。

今回の構成ではテストのツール例として **Vitest** を記載していますが、要件や言語によってその他のツールも考えられます。

## ビルド(Vite, etc.)

ソースコードから実行可能なプログラムを生成するプロセスのことです。

JavaScript だと [**webpack**](https://webpack.js.org/) というバンドルツールが有名ですが、新しいツールだと [**Vite**](https://ja.vitejs.dev/) や webpack の後継である [**Turbopack**](https://turbo.build/pack) が webpack よりも高速で注目を浴びています。Go だと標準でビルドの機能が用意されていたりします。

今回の構成では **Vite** を記載していますが、こちらは言語やツールの好みよって変わってくるでしょう。

## アプリケーションのデプロイ(Docker)

コードをサーバー上にアップロードして動かせるようにするプロセスのことです。

今回の構成ではコンテナを使用するアーキテクチャを想定しているので、デプロイのツールとしては [**Docker**](https://www.docker.com/ja-jp/) を記載しました。他にも [**AWS CLI**](https://aws.amazon.com/jp/cli/) といったコマンドの使用や [**Ansible**](https://www.ansible.com/) 、 [**AWS CodeDeploy**](https://aws.amazon.com/jp/codedeploy/) といったツールの使用、コンテナのアーキテクチャとして [**Kubernetes**](https://kubernetes.io/ja/) の使用も考えられます。

## インフラのプロビジョニング(Terraform)

コードを使用してインフラストラクチャのプロビジョニングを行います。いわゆる Infrastructure as Code（IaC）です。

[**Terraform**](https://www.terraform.io/) や [**AWS CDK**](https://aws.amazon.com/jp/cdk/) といったツールの使用が考えられますが、AWS 以外の SaaS にも使用したいため、今回は **Terraform** を記載しました。

**Terraform** のフォークサービスの [**OpenTofu**](https://opentofu.org/) というツールも登場したので、今後はこちらが主流になっていく可能性もありますね。

**Terraform** は今回紹介する下記の SaaS に対応しています。

- **Grafana Cloud**
- **AWS**
- **Checkly**
- **Sentry**
- **LaunchDarkly**

![](https://storage.googleapis.com/zenn-user-upload/478454c4465c-20240229.png)

## Grafana Cloud でオブザーバビリティを向上

**Grafana Cloud** を使用して監視とオブザーバビリティを向上します。「 [DevOps のケイパビリティ](https://zenn.dev/istone/articles/#devops-%E3%81%AE%E8%83%BD%E5%8A%9B%EF%BC%88%E3%82%B1%E3%82%A4%E3%83%91%E3%83%93%E3%83%AA%E3%83%86%E3%82%A3%EF%BC%89) 」における **モニタリングとオブザーバビリティ** や **システムをモニタリングして的確な判断** ・ **ビジュアル管理機能** ・ **障害の予兆通知** といったケイパビリティをサポートします。

## Grafana Cloud

**Grafana Cloud** は下記の７つのサービスを Grafana Labs がマネージドサービスとして提供している SaaS です。

- [**Grafana**](https://zenn.dev/istone/articles/#%E3%83%80%E3%83%83%E3%82%B7%E3%83%A5%E3%83%9C%E3%83%BC%E3%83%89%EF%BC%88grafana%EF%BC%89)
- [**Prometheus**](https://zenn.dev/istone/articles/#%E3%83%A1%E3%83%88%E3%83%AA%E3%82%AF%E3%82%B9\(prometheus\))
- [**Grafana Loki**](https://zenn.dev/istone/articles/#%E3%83%AD%E3%82%B0\(grafana-loki\))
- [**Grafana Tempo**](https://zenn.dev/istone/articles/#%E3%83%88%E3%83%AC%E3%83%BC%E3%82%B9\(grafana-tempo\))
- [**Grafana Pyroscope**](https://zenn.dev/istone/articles/#%E7%B6%99%E7%B6%9A%E7%9A%84%E3%83%97%E3%83%AD%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AA%E3%83%B3%E3%82%B0\(grafana-pyroscope\))
- [**Grafana OnCall**](https://zenn.dev/istone/articles/#%E3%82%AA%E3%83%B3%E3%82%B3%E3%83%BC%E3%83%AB\(grafana-oncall\))
- [**Grafana Incident**](https://zenn.dev/istone/articles/#%E3%82%A4%E3%83%B3%E3%82%B7%E3%83%87%E3%83%B3%E3%83%88%E7%AE%A1%E7%90%86\(grafana-incident\))
- [**Grafana k6**](https://zenn.dev/istone/articles/#%E8%B2%A0%E8%8D%B7%E3%83%86%E3%82%B9%E3%83%88\(grafana-k6\))

### Datadog との比較

前回の記事では、運用コストを考えると Datadog に１本化した方がいいのではないかというコメントをいくつかいただいたきました。今回の構成でも Sentry と Checkly の機能は Datadog に 1 本化できますが、Grafana OnCall や Grafana k6 に変わる機能が Datadog には無いので、今回の構成と同様の領域をカバーしようと思うと Datadog に１本化は出来ないことが分かります。

また、OSS の運用コストについても指摘もいただきましたが、Grafana Cloud は OSS を SaaS としているサービスなので、特に OSS の運用コストは発生していません。以前の記事では「ベンダーロックインを最小限にして OSS を使用する」ということを強調していたためにそういう印象を抱いてしまったと思うので、今回は「SaaS を組み合わせて DevOps を実現する」に修正します。

Datadog もかなり便利ではあるのですが、今回の構成と同じことを Datadog で実現しようと思うとかなり料金が膨れ上がりますし、Grafana の方がダッシュボードやアラートの自由度が高く使いやすい印象です。

## ダッシュボード（Grafana）

ダッシュボードは Grafana Cloud で提供されている **Grafana** を使用します。

### Grafana

**Grafana** とは Grafana Labs が公開しているデータ可視化の OSS です。

Grafana は様々なデータソースを可視化できるので、この Grafana を使用して様々なデータを可視化します。

![](https://storage.googleapis.com/zenn-user-upload/159d02b806bf-20240229.png)

Grafana Cloud 内のサービスだけでなく、データソースとして下記のサービスに対応しています。

- [**Amazon Athena**](https://zenn.dev/istone/articles/#aws-%E3%81%AE%E3%82%BB%E3%82%AD%E3%83%A5%E3%83%AA%E3%83%86%E3%82%A3%E3%81%A8%E3%82%B3%E3%82%B9%E3%83%88%E3%81%AE%E3%83%87%E3%83%BC%E3%82%BF\(amazon-athena\))
- [**Amazon API Gateway**](https://zenn.dev/istone/articles/#%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E3%83%87%E3%83%BC%E3%82%BF)
- [**AWS AppSync**](https://zenn.dev/istone/articles/#%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E3%83%87%E3%83%BC%E3%82%BF)
- [**Amazon RDS**](https://zenn.dev/istone/articles/#%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E3%83%87%E3%83%BC%E3%82%BF)
- [**Amazon OpenSearch Service**](https://zenn.dev/istone/articles/#%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E3%83%87%E3%83%BC%E3%82%BF)
- [**Sentry**](https://zenn.dev/istone/articles/#%E3%82%A8%E3%83%A9%E3%83%BC%E3%83%88%E3%83%A9%E3%83%83%E3%82%AD%E3%83%B3%E3%82%B0\(sentry\))

### アラート

また、Grafana にはデータソースのデータに対して閾値を設定してアラートを送信する機能もあります。

後述する [**Grafana OnCall**](https://zenn.dev/istone/articles/#%E3%82%A2%E3%83%A9%E3%83%BC%E3%83%88%E7%AE%A1%E7%90%86\(grafana-oncall\)) にアラートを送信することで、アラートを管理しやすくなります。

### Grafana のダッシュボードを Slack に送信

せっかく Grafana でダッシュボードを作成しても、ダッシュボードを確認する機会というのは残念ながら少ないだろうと思われます。  
ですが、 Grafana のダッシュボードのスクリーンショットを定期的に Slack に送信するようにすれば、ダッシュボードを確認する機会が増えるので、ダッシュボードの有効活用が期待できます。

2024 年 3 月現在、Grafana のダッシュボードのスクリーンショットを Slack に送信する機能というのは存在しませんが、メールで送信する機能は存在するのでこれを利用して Slack にダッシュボードのスクリーンショットを送信することが出来ます。

こちらのやり方についての記事を今後作成予定です。

## メトリクス(Prometheus)

メトリクス監視では Grafana Cloud の一部の機能として提供されている **Prometheus** というツールを使用します。ちなみに Prometheus は Grafana Labs の製品ではありません。

### Prometheus

**Prometheus** はメトリクスを収集する OSS で CNCF のプロジェクトです。Linux や Apache、MySQL 等のメトリクスを取得する様々な Exporter が用意されているので、目的に合ったメトリクスを収集することが出来ます。(Exporter は自分で作る事もできます。)  
Prometheus の可視化には通常、Grafana が利用されます。

### AWS のメトリクス

AWS のメトリクスの取得方法に関しては下記の公式ドキュメントを参照してください。

## ログ(Grafana Loki)

ログ監視では Grafana Cloud の一部の機能として提供されている **Grafana Loki** というツールを使用します。

### Grafana Loki

**Grafana Loki** は Grafana Labs が Prometheus を参考にして開発した、ログ収集を行う OSS です。

### AWS のログ

AWS のログの取得方法に関しては下記の公式ドキュメントを参照してください。

## トレース(Grafana Tempo)

トレース監視では Grafana Cloud の一部の機能として提供されている **Grafana Tempo** というツールを使用します。  
前述の [**OpenTelemetry SDK**](https://zenn.dev/istone/articles/#opentelemetry-sdk) から **Grafana Tempo** にトレースデータを送信します。

![](https://storage.googleapis.com/zenn-user-upload/d256f1c343f5-20240227.png)

### Grafana Tempo

**Grafana Tempo** は Grafana Labs が開発したトレース監視の OSS です。

## 継続的プロファイリング(Grafana Pyroscope)

Grafana Labs がオブザーバビリティの第４の柱と謳っている継続的プロファイリングを行うため、Grafana Cloud の一部の機能として提供されている **Grafana Pyroscope** を使用します。  
前述の [**Pyroscope SDK**](https://zenn.dev/istone/articles/#pyroscope-sdk) から **Grafana Pyroscope** にプロファイリングデータを送信します。

![](https://storage.googleapis.com/zenn-user-upload/f2ad034b21dd-20240227.png)

### Grafana Pyroscope

継続的プロファイリングで有名なツールの Pyroscope が、Grafana Labs に買収されたことにより **Grafana Pyroscope** になりました。

## 負荷テスト(Grafana k6)

システムに負荷をかけて、パフォーマンスの影響や不具合を確認するテストのことです。Grafana Cloud で利用できる **Grafana k6** を使用します。

Grafana Cloud 上の **Grafana k6** で実行するだけでなく、GitHub Actions 上で Grafana k6 CLI を動かして負荷テストを CI に組み込むこともできます。

![](https://storage.googleapis.com/zenn-user-upload/71355488e79b-20240326.png)

※ `$ k6 run` でローカルの実行、 `$ k6 cloud` でクラウド上での実行ができます。

### Grafana k6

JavaScript を用いて負荷試験のテストを行える k6 という OSS が、Grafana Labs に買収されたことにより **Grafana k6** になりました。

## アラート管理(Grafana OnCall)

Grafana Cloud で使用できる **Grafana OnCall** を使用して Grafana や Sentry などのアラートを管理します。Webhook 受信もできるので、GitHub Actions の失敗を管理するような使い方もできます。

![](https://storage.googleapis.com/zenn-user-upload/609c619a6d30-20240227.png)

### Grafana OnCall

**Grafana OnCall** は様々な監視ツールからのアラートを統合的に管理できる OSS です。Grafana のアラートだけでなく、AWS や Sentry 等のアラートにも対応しており、アラートの通知先には Slack 等のチャットツールや電話でのオンコールが利用できます。

重複したアラートをグルーピングする機能や、アラートの対応を記録できる機能があるので、ノイズになっているアラートが多すぎて重要なアラートに気付けないと言った [アラート疲れ](https://zenn.dev/istone/articles/#%E3%82%A2%E3%83%A9%E3%83%BC%E3%83%88%E7%96%B2%E3%82%8C) を防ぐことができます。

似たようなツールには [**PagerDuty**](https://www.pagerduty.co.jp/) や [**Opsgenie**](https://www.atlassian.com/ja/software/opsgenie) がありますが、Grafana OnCall はこれらのツールに比べて、費用が安いです。

## インシデント管理(Grafana Incident)

せっかくのインシデントを無駄にすることが無いよう、Grafana Cloud で使用できる **Grafana Incident** を使用してインシデントを管理します。

先ほどの **Grafana OnCall** やこちらの **Grafana Incident** には、アラートやインシデントが Resolve になるまでの時間を計測する機能があり、  
「 [Four Keys](https://zenn.dev/istone/articles/#devops-%E3%81%AE%E3%80%8Cfour-keys%E3%80%8D) 」の 4 つの指標のうち、 **サービスの復旧時間** を把握するために有用です。

## その他 AWS のデータを Grafana で可視化

## AWS のセキュリティとコストのデータ(Amazon Athena)

AWS のセキュリティデータには **Amazon Athena** と **Amazon Security Lake** 、コストデータには **Amazon Athena** と **AWS Data Export** を使用します。

![](https://storage.googleapis.com/zenn-user-upload/34b576f20c6c-20240227.png)

Grafana のデータソースプラグインとして **Amazon Athena** が用意されているので、これらのデータを可視化できます。

### Amazon Athena

**Amazon Athena** は SQL を使用して Amazon S3 内のデータを直接分析できる AWS のサービスです。これを使用して S3 に保存されているセキュリティデータやコストデータを参照します。

### Amazon Security Lake

**AWS Security Lake** は AWS Security Hub や AWS CloudTrail 等の様々なセキュリティログを Open Cybersecurity Schema Framework (OCSF)というオープンソーススキーマの形式で保存し、集約・管理できるサービスです。AWS 以外のサービスにも対応しています。

### AWS Data Exports

請求やコスト管理に関するデータを S3 バケットに定期的に配信できます。

### Athena のデータを Grafana で可視化

Grafana には Athena をデータソースとして可視化するためのプラグインが用意されています。

## アプリケーションのデータ

運用上アプリケーションのデータを可視化したいケースもあるかと思いますが、様々な AWS サービスを Grafana のデータソースプラグインを使用して、可視化できます。

### Amazon API Gateway, AWS AppSync のデータを Grafana で可視化

HTTP API や GraphQL 用の Infinity というプラグインを使用して可視化できます。

### Amazon RDS のデータを Grafana で可視化

MySQL や PostgreSQL 用のプラグインを使用して可視化できます。

### Amazon OpenSearch Service のデータを Grafana で可視化

Elasticsearch や OpenSearch 用のプラグインを使用して可視化できます。

## その他 SaaS で DevOps を強化

GitHub や Grafana Cloud では補えない機能を、他の SaaS を使用して補完します。

## セキュリティスキャン(Snyk)

セキュリティの脆弱性を検出し、アプリケーションの安全性を確保することです。 **Snyk** というツールを使用します。「 [DevOps のケイパビリティ](https://zenn.dev/istone/articles/#devops-%E3%81%AE%E8%83%BD%E5%8A%9B%EF%BC%88%E3%82%B1%E3%82%A4%E3%83%91%E3%83%93%E3%83%AA%E3%83%86%E3%82%A3%EF%BC%89) 」における **セキュリティのシフトレフト** に関するケイパビリティをサポートします。

GitHub Actions 上で Snyk CLI を動かして脆弱性スキャンを CI に組み込んだり、Web 上の **Snyk** で定期的な脆弱性スキャンを行う事もできます。

![](https://storage.googleapis.com/zenn-user-upload/f75454315c65-20240326.png)

※ `$ snyk test` で脆弱性スキャンをローカル実行、 `$ snyk monitor` で Web 上の Snyk にプロジェクトを作成して、継続的な脆弱性スキャンを行うことができます。

下記画像はアジャイルテストの４象限と呼ばれるものです。

![](https://storage.googleapis.com/zenn-user-upload/5820d2f44e36-20240302.png)

非機能テストにはパフォーマンスやセキュリティのテストが含まれ、こちらをすでに紹介した [**k6**](https://zenn.dev/istone/articles/#%E8%B2%A0%E8%8D%B7%E3%83%86%E3%82%B9%E3%83%88\(grafana-k6\)) やこの [**Snyk**](https://zenn.dev/istone/articles/#%E3%82%BB%E3%82%AD%E3%83%A5%E3%83%AA%E3%83%86%E3%82%A3%E3%82%B9%E3%82%AD%E3%83%A3%E3%83%B3\(snyk\)) でカバーしています。

今回は **Snyk** を使用しますが、その他にも [**Trivy**](https://trivy.dev/) や GitHub より提供されている [**Dependabot**](https://docs.github.com/ja/code-security/dependabot/working-with-dependabot) や [**CodeQL**](https://docs.github.com/ja/code-security/code-scanning/introduction-to-code-scanning/about-code-scanning-with-codeql) といったサービスの利用が考えられます。  
それぞれ脆弱性として認識される項目が違ったりするので、よりセキュリティを強化したいなら単体のツールを使用するのではなく、複数組み合わせてもいいでしょう。

### Snyk

**Snyk** はアプリケーションの脆弱性を検知するための SaaS で、以下の 4 つの機能があります。

- Snyk Open Source: オープンソースコードの脆弱性を検知
- Snyk Code: アプリケーションコードの脆弱性を検知
- Snyk Container: コンテナイメージの脆弱性を検知
- Snyk Infrastructure as Code: Kubernetes、Terraform 等の設定ファイルの脆弱性を検知

## コードレビュー(CodeRabbit)

**CodeRabbit** を使って AI によるコードレビューをしてもらいます。「 [DevOps のケイパビリティ](https://zenn.dev/istone/articles/#devops-%E3%81%AE%E8%83%BD%E5%8A%9B%EF%BC%88%E3%82%B1%E3%82%A4%E3%83%91%E3%83%93%E3%83%AA%E3%83%86%E3%82%A3%EF%BC%89) 」における **変更承認の効率化** に関するケイパビリティをサポートします。

PR のレビューはレビュー側にも知識が必要ですし、規模の大きい PR はレビューをするのも大変なので、 **CodeRabbit** を使って PR のレビューを効率化させます。

### CodeRabbit

**CodeRabbit** は PR の要約と AI によるレビューをしてくれる SaaS です。

AI もまだまだ完璧ではないので、レビューを全て **CodeRabbit** に丸投げするというのは難しいです。  
しかし、要約と AI によるレビューがあるだけで、PR のレビューをかなり効率化できますし、人間によるレビューだけの時よりもコード品質の向上に期待できます。

## テストケースの管理(Qase)

**Qase** を使ってテストケースの管理をします。「 [DevOps のケイパビリティ](https://zenn.dev/istone/articles/#devops-%E3%81%AE%E8%83%BD%E5%8A%9B%EF%BC%88%E3%82%B1%E3%82%A4%E3%83%91%E3%83%93%E3%83%AA%E3%83%86%E3%82%A3%EF%BC%89) 」における **チームのテスト** に関するケイパビリティをサポートします。

単体テストや結合テスト、E2E テストを自動化させましたが、全てのテストを自動化できるわけではありません。また、手動によるテストによって自動テストでは明らかにならなかったような問題を発見できることもあります。

すでに紹介したアジャイルテストの４象限では、機能テストの一部や探索的テストは手動で行うものとされています。

![](https://storage.googleapis.com/zenn-user-upload/5820d2f44e36-20240302.png)

スプレットシート等を使用するようなケースが多いかと思いますが、 **Qase** を使うことでテストケースの管理を効率化できます。

### Qase

**Qase** はテストケースの管理をするための SaaS です。

[**Jest**](https://jestjs.io/ja/) や [**Playwright**](https://playwright.dev/) のテスト結果を **Qase** に送信することも出来ます。

## 外形監視と E2E テスト(Checkly)

外形監視とは、外部からのユーザー視点でアプリケーションの監視をすることです。Grafana Cloud にも外形監視は用意されていますが、機能としてはまだ不十分なので、 **Checkly** というツールを使用します。

また、E2E テストとは、ソフトウェアがエンドユーザーの視点で正しく機能するかを確認するテストのことです。  
[**Playwright**](https://playwright.dev/) といったツールが有名で、 **Checkly** というツールにはこの **Playwright** が組み込まれているので、E2E テストにもこの **Checkly** を使用します。

GitHub Actions 上で Checkly CLI を動かして外形監視と E2E テストを CI に組み込んだり(E2E テストに関しては直接 Playwight の CLI を動かすのでも可)、Web 上の **Checkly** で定期的な外形監視と E2E テストを行う事もできます。

![](https://storage.googleapis.com/zenn-user-upload/4ca482d3189f-20240326.png)

※ `$ checkly test` で外形監視と E2E テストをローカル実行、 `$ checkly deploy` で Web 上の Checkly にデプロイして、継続的な外形監視と E2E テストを行うことができます。

### 外形監視と E2E テストの違い

外形監視と E2E テストは似てますが、外形監視は実稼働環境でアプリを継続的にテストすることを目的としており、E2E テストはデプロイ前にバグを検出することを目的としています。

### Checkly

**Checkly** は外形監視、E2E テストが行える SaaS です。E2E テストには [**Playwright**](https://playwright.dev/) を使用します。

[**外形監視と E2E テストができる Checkly とは？**](https://zenn.dev/istone/articles/whats-checkly) という記事にて Checkly の機能について詳しく紹介しているので、こちらもご覧いただけると幸いです。

### Datadog との比較

Datadog との比較はこちらのサイトをご覧ください。Checkly は Datadog と比較してかなり安価であることが分かります。

### Checkly と Prometheus の統合

チェックの結果を Prometheus 形式のメトリクスとして出力できるので、Grafana にて結果を確認できます。

Grafana Cloud で Checkly の Prometheus エンドポイントからメトリクスをスクレイピングします。

![](https://storage.googleapis.com/zenn-user-upload/3aa71a30ee3c-20240229.png)

## エラートラッキング(Sentry)

前述の [**Sentry SDK**](https://zenn.dev/istone/articles/#sentry-sdk) から RUM (Real User Monitoring)のメトリクスやエラートラッキングしたデータをこの **Sentry** に送信します。

![](https://storage.googleapis.com/zenn-user-upload/384bf453dd91-20240227.png)

### Sentry

**Sentry** はパフォーマンス監視やエラー監視を行うための SaaS です。

### Sentry のデータを Grafana で可視化

Grafana は Sentry のデータソースプラグインが用意されているので、Sentry のデータを Grafana で可視化できます。

また Sentry のアラートを Grafana OnCall に送信できます。これで Sentry のアラートも管理しやすくなります。

## フィーチャーフラグ(LaunchDarkly)

前述の [**OpenFeature SDK**](https://zenn.dev/istone/articles/#openfeature-sdk) をこの **LaunchDarkly** で管理して、フィーチャフラグを実現します。

![](https://storage.googleapis.com/zenn-user-upload/a910bbea350f-20240227.png)

### LaunchDarkly

**LaunchDarkly** はフィーチャーフラグ管理のための SaaS で前述の **OpenFeature** に対応しています。

### LaunchDarkly と Grafana の統合

LunchDarkly には Grafana との統合が用意されており、こちらを利用することでフィーチャーフラグの変更を Grafana ダッシュボードの注釈として表示できます。  
「 [Four Keys](https://zenn.dev/istone/articles/#devops-%E3%81%AE%E3%80%8Cfour-keys%E3%80%8D) 」の 4 つの指標のうち、 **変更失敗率** を把握するためにも有用です。

## Slack で ChatOps を実現

アラートは基本的に全て **Slack** に送信して、ChatOps を実現します。

![](https://storage.googleapis.com/zenn-user-upload/51a089c3d833-20240227.png)

## ChatOps

**ChatOps** とは運用に関わる様々なタスクを、Slack 等のチャットツールを使用して効率化することで、SaaS との連携による業務効率化、自動化、情報収集の容易化を実現できます。  
主なメリットとして、インタラクティブな操作による運用が行える事や、通知の迅速な対応、共有と記録の容易さがあげられます。

DevOps の **文化** を育むためにも、ChatOps は非常に重要です。

## DevOps のツールに正解はない

「 [DevOps は”文化”](https://zenn.dev/istone/articles/#devops-%E3%81%AF%E2%80%9D%E6%96%87%E5%8C%96%E2%80%9D) 」でも紹介したように、ツールは **文化** を加速させるためのものです。あくまでもツールは手段であり、目的ではありません。

また、 DevOps のツールに正解はありません。「 [Effective DevOps](https://www.oreilly.co.jp/books/9784873118352/) 」ではツールの誤解として、下記を挙げています。

> **技術 *X* から、他社に合わせて技術 Y に移行しなければいけない**

→ 技術の変更にはコストがかかります。

> **技術 *X* を使っているので、うちは devops を実践している**

→ DevOps に役立つツールや技術は確かにありますが、それらのツールや技術がなぜ役に立つのかを理解するのが大切です。

> **間違ったツールを選ばないように注意しなければならない**

→ 間違ったツールを選んだからといって失敗する訳ではありません。

> **DevOps ツール全部入りセットや devops-as-a-Service を購入すればよい**

→ 最新の素晴らしい DevOps のツールを持っているだけでは不十分で、成功するにはツールを効果的に使わなければなりません。

DevOps 実現構成というタイトルにしましたが、今回紹介した SaaS を採用したからといって DevOps が成功するわけではありません。  
現在の組織に合った適切なツールを選択して、使用するツールや技術についてしっかりと理解し、効果的に活用する事が重要なのです。

## さいごに

今回は DevOps についてと様々なツールを紹介しました。

[![](https://res.cloudinary.com/zenn/image/fetch/s--x1IyUiZt--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_1200/https://images.microcms-assets.io/assets/0402567430be43b4a7db9f7365e62718/7f2db45ddd184d5389f0d1f3a1874c6c/devops.drawio.png)](https://images.microcms-assets.io/assets/0402567430be43b4a7db9f7365e62718/7f2db45ddd184d5389f0d1f3a1874c6c/devops.drawio.png)

こちらはあくまでも 2024 年 3 月時点での構成なので、今後もどんどん更新していく(もしくは新しい記事を作成する)予定です。また、今回の構成に関連する記事も書いていこうと思うので、そちらもお読みいただければ幸いです！

## 書籍紹介

今回の記事で登場した書籍です。

- [The DevOps 　逆転だ！究極の継続的デリバリー](https://amzn.asia/d/7zvMDaT)
- [The DevOps ハンドブック 理論・原則・実践のすべて](https://amzn.asia/d/7UUYl86)
- [Lean と DevOps の科学](https://amzn.asia/d/2sEB6hC)
- [Effective DevOps](https://www.oreilly.co.jp/books/9784873118352/)
- [システム運用アンチパターン](https://www.oreilly.co.jp//books/9784873119847/)
- [ソフトウェアアーキテクチャメトリクス](https://www.oreilly.co.jp/books/9784814400607/)

下記書籍も大変参考になります。

- [入門 監視](https://www.oreilly.co.jp/books/9784873118642/)
- [オブザーバビリティエンジニアリング](https://www.oreilly.co.jp/books/9784814400126/)
- [マイクロサービスアーキテクチャ](https://www.oreilly.co.jp/books/9784814400010/)

## 記事紹介

今回紹介したサービスについてより詳しく知りたい方は下記の記事をご覧ください。

- **GitHub Actions**
	- [Git Hub Actions 入門](https://zenn.dev/hashito/articles/7c292f966c0b59)
	- [GitHub Actions って何？触ってみて理解しよう！入門・逆引きリファレンス](https://qiita.com/yu-ichiro/items/b50ceb0008edc3c0312e)
- **Prometheus**
	- [PromQL 事始め](https://qiita.com/tatsurou313/items/64fcaae3567f24d13dd5)
- **Grafana Loki**
	- [最短で理解して運用する Grafana Loki](https://zenn.dev/taisho6339/articles/0654040691aaab)
- **Grafana k6**
	- [負荷テストツール「k6」入門](https://zenn.dev/pharmax/articles/98ed49994cdaf2)
- **Snyk**
	- [Snyk 無償版を使ってみた](https://qiita.com/kannkyo/items/913055157c9105d02926)
	- [Snyk はじめまして: 開発者フレンドリーなセキュリティ脆弱性の管理](https://zenn.dev/cureapp/articles/snyk-security-101)
- **CodeRabbit**  
	- [もう初回コードレビューは AI に任せる時代になった - CodeRabbit -](https://zenn.dev/minedia/articles/7928ef7545b393)
	- [CodeRabbit を１ヵ月開発チームで実際に使ってみました！](https://zenn.dev/lovegraph/articles/48a3b7288299a2)
- **Qase**
	- [テスト管理ツール Qase のメリット/デメリット](https://zenn.dev/spacemarket/articles/e5be4cd52c8387)
	- [テスト管理ツール「Qase」を使ってスプレッドシートのテスト管理から脱出しようとした話](https://qiita.com/henjiganai/items/9fadf6d1099357b49e9c)
- **Playwright**
	- [Playwright も知らないで開発してる君たちへ](https://qiita.com/cc822jp/items/6f786a9ed104af1a382f)
- **Sentry**
	- [エラー監視には Sentry が超便利！](https://qiita.com/Chanmoro/items/a9cbde57fd6c0926b5b4)
	- [フロントエンド監視の全体像と実現方法](https://zenn.dev/kimitsu/articles/frontend-monitoring)
- **LaunchDarkly**
	- [LaunchDarkly による Feature Flags 制御の基礎](https://zenn.dev/microcms/articles/feature-flags-control-by-launchdarkly-basic)
	- [LaunchDarkly を入れてフィーチャーフラグの運用を改善した話](https://techblog.gaudiy.com/entry/2021/12/08/135920)

また、今回の構成に関連した記事をいくつか書いているので、そちらもご覧いただければ幸いです。

- [GitHub Actions のログを Grafana Loki に送信するアクションを作成した](https://zenn.dev/istone/articles/send-log-to-loki)
- [外形監視と E2E テストができる Checkly とは？](https://zenn.dev/istone/articles/whats-checkly)
- Grafana のダッシュボードを Slack に投稿する（メールの画像を Slack に投稿する）(近日公開)
- アラートの管理に便利な「Grafana OnCall」を使ってみよう(近日公開)

[GitHubで編集を提案](https://github.com/istone-you/zenn/blob/main/articles/297833b006dfd6.md)

223

7