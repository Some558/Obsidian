---
title: "ポートフォリオサイトにmicroCMS導入してみた"
source: "https://qiita.com/saku6911/items/e46f7069fa340fee9396"
author:
  - "[[saku6911]]"
published: 2025-05-23
created: 2025-05-24
description: "はじめにゆかっしゅです。2021年に事務職からデザイナー/コーダーにジョブチェンジをし、現在はフロントエンドエンジニアにスキルアップするべく、モダンフロントエンドを学習しています。今回は先月作…"
tags:
  - "clippings"
---
![](https://relay-dsp.ad-m.asia/dmp/sync/bizmatrix?pid=c3ed207b574cf11376&d=x18o8hduaj&uid=)

## エンジニアとしての市場価値を測りませんか？PR

企業からあなたに合ったオリジナルのスカウトを受け取って、市場価値を測りましょう

[無料でForkwellに登録する](https://lp.recruiting.forkwell.com/scout?argument=249xHStF&dmai=a67f4ef09e582b)

## はじめに

ゆかっしゅです。  
2021年に事務職からデザイナー/コーダーにジョブチェンジをし、現在はフロントエンドエンジニアにスキルアップするべく、モダンフロントエンドを学習しています。  
今回は先月作成したポートフォリオサイトの「仕事で経験した成果」や「学習で得た経験」の部分をCMS化していきたいと思います。

今回は **ヘッドレスCMS** の **micro CMS** を使用していきたいと思います。

## ヘッドレスCMSとは

CMS（Contents Management System）とは、Webサイト構成するコンテンツ（テキストや画像、デザイン・レイアウト情報）などを一元的に保存・管理するシステムのことです。

個人的なイメージとしては、CMSを使わないWEB制作は **「布からTシャツを作る」イメージ。**  
CMSを使用したWEBサイト制作は **「出来上がったTシャツから何を使うか選んでコーディネートを考える」イメージです。**

代表的なCMSとしては **WordPress** が一番有名だと思います。

CMSは基本的にフロントエンドとバックエンドの機能が備わっていますが、  
フロントエンドの機能がなくバックエンドの機能のみもつCMSを **ヘッドレスCMS** といいます。  
どういうことかというと、見た目は自分で作るということです。（WordPressでもテーマ作ったりしますが...）

ヘッドレスCMSのサービスを利用してブログの記事を書き、そのブログ記事のデータをAPIをたたいて取得して画面上に表示させます。  
先ほどのTシャツの例えでいうとヘッドレスCMSは **「白い半袖のTシャツがあって、デザインは自分で描ける」みたいなイメージです。**

なのでヘッドレスCMS導入の際はある程度のフロントエンドの知識が必要になります。

## ヘッドレスCMSのメリット・デメリット

### メリット

- **好きなフロントエンド技術で開発できる**  
	CMSだとフロントエンドがCMS特有の技術に縛られることが多いです。ヘッドレスCMSはReact、Vue、Next.js、Nuxt など好きな技術でフロントの開発が可能です。
- **高い拡張性と柔軟性**  
	APIでデータ取得するため、モバイルアプリ・Webサイト・サイネージなど多方面に展開可能
- **パフォーマンス最適化がしやすい**  
	フロントをJamstack構成（静的生成など）にすれば高速表示が可能です。

### デメメリット

- **フロントエンドの知識が必要**  
	フロントエンドを自作する必要があるため、エンジニアの知識が必要です。
- **管理画面の柔軟性に差がある**  
	管理UIがCMSごとに異なり、編集者向けに使い勝手の調整が必要になることもある
- **CMSによっては有料**  
	ContentfulやSanityは一定以上の機能で有料プランに移行する

## microCMS導入してみよう

### 利用技術

React(19.0.0)  
TypeScript(5.0)  
Next.js(15.3.1)  
Tailwindcss(4.0)  
microcms-js-sdk（3.2.0）  
Vercel

### microCMSに会員登録

ポートフォリオくらいの小規模開発であれば無料で利用できます。  
一部機能は課金制のようです。

### microCMSの設定

基本は下記ドキュメントを参考に設定を進めていきます。  
私はnextjs(13以上）を使用しているのでnextjsを選択しApp Routerのページを参考にします。

流れとしては「サービスの作成→APIの作成→APIスキーマの作成→コンテンツ（記事）の作成」をおこないます。

### プロジェクトでの設定

まずは環境変数を設定します。

.env.local

```typescript
MICROCMS_API_KEY=xxxxxxxxxx(あなたのサービスのAPIキー）
MICROCMS_SERVICE_DOMAIN=xxxxxxxxxx(あなたのサービスのドメイン）
```

ちなみにAPIキー（赤）とドメイン（青）はここに記載されています。  
[![スクリーンショット 2025-05-23 145714.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4068307/c69f577e-70b8-4478-b59f-fcb486488976.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F4068307%2Fc69f577e-70b8-4478-b59f-fcb486488976.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=c3b777bafa922af1bb6495b59a5ade2d)

次にmicrocms-js-sdkをインストールします。

```text
npm install microcms-js-sdk
```

そしてlibsディレクトリにmicrocms.tsを作成します。

.env.local

```typescript
// libs/microcms.ts
import { createClient } from 'microcms-js-sdk';

// 環境変数にMICROCMS_SERVICE_DOMAINが設定されていない場合はエラーを投げる
if (!process.env.MICROCMS_SERVICE_DOMAIN) {
  throw new Error('MICROCMS_SERVICE_DOMAIN is required');
}

// 環境変数にMICROCMS_API_KEYが設定されていない場合はエラーを投げる
if (!process.env.MICROCMS_API_KEY) {
  throw new Error('MICROCMS_API_KEY is required');
}

// Client SDKの初期化を行う
export const client = createClient({
  serviceDomain: process.env.MICROCMS_SERVICE_DOMAIN,
  apiKey: process.env.MICROCMS_API_KEY,
});
```

あとはデータを取得するコードを書いて一覧表示や詳細ページの表示を行います。  
私は関心の分離の観点からデータ取得のコードは分けて書きました。

getInformation.tsx

```typescript
import { client } from '../libs/microcms';

type Post = {
  id: string;
  body:string;
  title: string;
  publishedAt: string;
  thumbnail: {
    url: string;
    height: number;
    width: number;
  };
  categories: {
    id: string;
    name: string;
  }[];
  skill: string;
};

export async function getWorkPosts(): Promise<Post[]> {
  const data = await client.get({
    endpoint: 'work',
    queries: {
      fields: 'id,title,thumbnail,categories,skill',
      depth: 1,
    },
  });
  return data.contents;
}

export async function getWorkPagePosts(id: string): Promise<Post> {
  const data = await client.get({
    endpoint: \`work/${id}\`,
  });
  return data;
}

export async function getLearningPosts(): Promise<Post[]> {
  const data = await client.get({
    endpoint: 'learning',
    queries: {
      fields: 'id,title,thumbnail,categories,skill',
      depth: 1,
    },
  });
  return data.contents;
}

export async function getLearningPagePosts(id: string): Promise<Post> {
  const data = await client.get({
    endpoint: \`learning/${id}\`,
  });
  return data;
}
```

私は学習ページと仕事ページ二つのAPIを使用していたのでWorkとLearningで分かれています。  
詳細ページはdynamic routesになるので\[id\]が出てきます。  
下記画像に記載されているコンテンツIDが\[id\]になります。

[![スクリーンショット 2025-05-23 150857.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4068307/4b179b8b-8680-4374-8924-e17a6526133e.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F4068307%2F4b179b8b-8680-4374-8924-e17a6526133e.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=2ba1c53d28c675983cf39cad9270317d)

### データ取得はクライアント側では書けない

これはnextのApp Routerを使用している際の注意点です。  
一覧表示の際に先ほど記載したデータ取得の関数を使うのですが、クライアント側ではこの関数は使えません。  
私はsiwiperを一覧表示で使用していたので、 `"use client";`を記載していてエラーになりました。  
クライアントとサーバーでコンポーネントを分けることでエラーが解決します。

workClient.tsx

```typescript
"use client";

import { Swiper, SwiperSlide } from "swiper/react";
import "swiper/css";
import "swiper/css/navigation";
import "swiper/css/pagination";
import { Navigation, Pagination } from "swiper/modules";
import Heading from "../../ui/heading/page";
import WorkCard from "../../ui/workCard/page";
import { Fade } from "react-awesome-reveal";

type WorkProps = {
  posts: {
    id: string;
    title: string;
    thumbnail: { url: string };
    skill: string;
    categories: {
      id: string;
      name: string;
    }[];
  }[];
};
export default function WorkClient({ posts }: WorkProps) {
  return (
    <div className="w-4/5 mx-auto py-15 md:py-24" id="work">
      <Fade direction="up" triggerOnce cascade damping={0.3}>
        <Heading headingEn="Work" headingJa="仕事成果" />
        <Swiper
          modules={[Navigation, Pagination]}
          navigation={true}
          spaceBetween={24}
          slidesPerView={3}
          grabCursor={true}
          pagination={{ clickable: true }}
          className="h-120 w-full"
          breakpoints={{
            350: { slidesPerView: 1 },
            780: { slidesPerView: 2, spaceBetween: 32 },
            1200: { slidesPerView: 3, spaceBetween: 32 },
            1500: { slidesPerView: 4 },
          }}
        >
          {posts.map((post) => (
            <SwiperSlide key={post.id}>
              <WorkCard
                id={post.id}
                imgSrc={post.thumbnail.url}
                imgAlt="ブログのサムネイル画像"
                heading={post.title}
                skill={post.skill}
                categories={post.categories}
              />
            </SwiperSlide>
          ))}
        </Swiper>
      </Fade>
    </div>
  );
}
```

page.tsx

```typescript
import { getWorkPosts } from "../../../services/getInformation";
import WorkClient from "./workClient";

export default async function Work() {
  const posts = await getWorkPosts();
  return <WorkClient posts={posts} />;
}
```

[0](https://qiita.com/saku6911/items/#comments)

新規登録して、もっと便利にQiitaを使ってみよう

1. あなたにマッチした記事をお届けします
2. 便利な情報をあとで効率的に読み返せます
3. ダークテーマを利用できます
[ログインすると使える機能について](https://help.qiita.com/ja/articles/qiita-login-user)

[新規登録](https://qiita.com/signup?callback_action=login_or_signup&redirect_to=%2Fsaku6911%2Fitems%2Fe46f7069fa340fee9396&realm=qiita) [ログイン](https://qiita.com/login?callback_action=login_or_signup&redirect_to=%2Fsaku6911%2Fitems%2Fe46f7069fa340fee9396&realm=qiita)

[![saku6911](https://qiita-user-profile-images.imgix.net/https%3A%2F%2Fs3-ap-northeast-1.amazonaws.com%2Fqiita-image-store%2F0%2F4068307%2F9291915af130acbb3baa5534287e72b6774395e2%2Flarge.png%3F1745371464?ixlib=rb-4.0.0&auto=compress%2Cformat&lossless=0&w=128&s=6c6e7bf1f78e51822788c9e735597584)](https://qiita.com/saku6911)

[

## @saku6911(しらとり ゆか)

](https://qiita.com/saku6911)

フロントエンドエンジニアを目指してます。

[Web](https://portfolio-site-git-master-saku6911s-projects.vercel.app/) [RSS](https://qiita.com/saku6911/feed)

[4](https://qiita.com/saku6911/items/e46f7069fa340fee9396/likers)

3