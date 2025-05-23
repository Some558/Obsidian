---
title: "技術書ランキングサイトをQiita記事の集計から作ったら、約4000冊の技術本がいい感じに並んだ"
source: "https://qiita.com/jabba/items/edefda09121877b79760"
author:
  - "[[Qiita]]"
published: 2023-02-16
created: 2025-05-15
description: "QiitaのAPIから投稿記事を取り出し、技術書籍を紹介している箇所を集計して、ランキングサイトを作った。作った本人が言うのも何だけど、できあがった技術書ランキングがやたらエンジニア指向で便利で面白…"
tags:
  - "clippings"
---
![](https://relay-dsp.ad-m.asia/dmp/sync/bizmatrix?pid=c3ed207b574cf11376&d=x18o8hduaj&uid=3790085)

この記事は最終更新日から1年以上が経過しています。

QiitaのAPIから投稿記事を取り出し、技術書籍を紹介している箇所を集計して、ランキングサイトを作った。作った本人が言うのも何だけど、できあがった技術書ランキングがやたらエンジニア指向で便利で面白いなー、と。

[技術書ランキングをQiita記事の集計から作成した  
テック・ブック・ランク](https://techbookrank.com/)

エンジニアにとって技術書の選定はまーまー苦労する。単なる発行部数ランキングでは「人気あるからって技術書として参考になるとはかぎらない」と、なってしまいがち。ブログでオススメされている書評なんかも参考にするが、結局それらは書評を書いた人の主観で書かれたのであって客観的指標にはなりえない。  
そこで「Qiitaにある技術ブログ記事内で紹介されている書籍情報を集計すればひと味違った書籍ランキングになるのでは？」と考えた。

で、以下の条件に当てはまる本を「いい本」とした

- たくさんのQiita記事で紹介されている本
- 人気のあるQiita記事で紹介されている本
- 新しい記事で紹介されている本

結果としてできあがったランキングの総合部門トップ６はこんな感じになった。当たり前だけど「売れてる本」と「技術記事で紹介したい本」はちょっと違う。本当の意味で **有用な技術本** というのは後者の「紹介したい本」の要素が多いかな、と。

[![og_image.png](https://qiita-image-store.s3.amazonaws.com/0/108761/e422f7ad-981e-122e-5816-ef9bf653bc76.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.amazonaws.com%2F0%2F108761%2Fe422f7ad-981e-122e-5816-ef9bf653bc76.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=bbf125365c30b1be849313184afd4f7b)

いい感じに古くからずっと支持されている古典的名書と最新の人気ある書籍がトップに入っている。「 [リーダブルコード](https://techbookrank.com/books/5ab6c45330e8410004196087) 」なんかはいつまでも廃れることのない名著だし、最近出たばかりの「 [エンジニアリング組織論への招待](https://techbookrank.com/books/5ab6c3de30e8410004195c10) 」や [@jnchitoさん](https://qiita.com/jnchito) の「 [プロを目指す人のためのRuby入門](https://techbookrank.com/books/5ab6df0a30e841000419eabb) 」がトップ１０に入っていて、気に入っている。ちなみに恣意的に特定の本のランクを上げたりは絶対にしていない。同じルールの元で公平に集計測定した結果がこれ。

Qiita記事にあるタグがいい効果を発揮している。Qiita記事に貼ってあるタグはそのまま紹介されている書籍のタグとした。つまりタグ=>記事=>書籍となっているのでタグと書籍の関係は直接ではなく、ゆるーく繋がっているだけ。そこがいいなと思っている。

例えば「 [人工知能は人間を超えるか](https://techbookrank.com/books/5ab6c69b30e84100041972d3) 」という本の場合、この本には２０以上のタグが付いている。

[![Screen Shot 2018-04-05 at 09.47.04.png](https://qiita-image-store.s3.amazonaws.com/0/108761/7f60d34d-8f71-61b8-c8ae-16874cfbbc19.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.amazonaws.com%2F0%2F108761%2F7f60d34d-8f71-61b8-c8ae-16874cfbbc19.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=2eb50aa7e849d2cbc6b8c8bdd093fd33)

ウェブサイトで見ていただくとドーナツグラフでタグの分析結果が見れるようにした。

PythonやTesorFlowのタグが付いているが本書にはこれらの技術に関する言及は無い。でもタグがあって、それは「この本を紹介するエンジニアはだいたいPythonやTesorFlowに関係する記事を書いてますよ」という意味になる。このゆるーい関係のタグ付けがいいと思った。他にもRubyの本にGitHubがタグ付けされていたり、書籍の内容には関係無さそうだけど実務では関係あるタグ付けがなされている。

自分で作ったサイトながら、そのタグをクリックして関連タグで人気順にソートされた技術本ランキングを次々に眺めるのが面白くて、しばらくサイト内を巡回していた。例えばAという技術のタグを押しても全てがAに関する書籍ではなかったりするので、 **「おーこんな本もあったのか」** という発見がある。なのでタグを目立つようにして、検索窓は右上に必要な時だけ表示する仕組みにした。サイトのコンセプトとして検索してピンポイントで必要な書籍情報だけを見るよりも、タグをクリックしていろいろ巡回して見た方がこのサイトは面白いと思ったからだ。

本についてはその本を読むこと以前に「その本との出会い」がとても重要だと思っている。売れている順や人気順のランキングならばアマゾンので十分だ。  
テック・ブック・ランクは他には無い「本との出会い」がある。なぜならそのランキングに使っている指標が限りなくエンジニア目線を元にした指標だからだ。人工知能の本にTesorFlowのタグを付ける、なんてやるのはエンジニアだけだろう。

Qiitaの技術記事ってそれなりにちゃんと書かないとLike数なりView数なりで人気を得ることは難しい。なのでそれらと連動した技術本のランキングもそれなりに信用に値するかな、と思っている。

それとご自身で投稿したQiita記事で技術本を紹介されていたら、それが [テック・ブック・ランク](https://techbookrank.com/) にちゃんと反映されているか確かめてみたら面白いかも。というかもし反映されてなかったら、ご連絡いただければ幸いです。APIからの本のリンク読み取りっていろいろ種類があって全てはカバーできていないので。

[テック・ブック・ランク](https://techbookrank.com/) が皆さんの **「こんな本があったのか！」** をたくさん提供することを願って公開した。ご感想なり、批評なりなんでもコメントください。

[技術書ランキングをQiita記事の集計から作成した  
テック・ブック・ランク](https://techbookrank.com/)

### テック・ブック・ランクのサイト構築に使った技術

- Rails
- GraphQL
- React + Redux
- Google Cloud Platform
- AWS S3
- Heroku
- CloudFlare

### 公開した後のこと

[開設後３週間で収益１０万円を得た個人開発サイトでやったことの全部を公開する](https://qiita.com/jabba/items/1a49e860a09a613b09d4)

[18](https://qiita.com/jabba/items/#comments)

コメント一覧へ移動

[1744](https://qiita.com/jabba/items/edefda09121877b79760/likers)

いいねしたユーザー一覧へ移動

1636