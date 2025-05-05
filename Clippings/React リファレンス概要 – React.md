---
title: "React リファレンス概要 – React"
source: "https://ja.react.dev/reference/react"
author:
  - "[[@reactjs]]"
published:
created: 2025-05-05
description: "The library for web and native user interfaces"
tags:
  - "clippings"
---
このセクションは React で開発をする際の詳細なリファレンスドキュメントです。React の使い方の概要については [Learn](https://ja.react.dev/learn) セクションをご覧ください。

React リファレンスは機能別にいくつかのサブセクションに分かれています。

## React

プログラムから利用する React の機能です。

- [フック](https://ja.react.dev/reference/react/hooks) - コンポーネント内から使用する様々な React の機能
- [コンポーネント](https://ja.react.dev/reference/react/components) - JSX 内で用いる組み込みコンポーネント
- [API](https://ja.react.dev/reference/react/apis) - コンポーネントの定義に用いる API
- [ディレクティブ](https://ja.react.dev/reference/rsc/directives) - React Server Components 互換のバンドラに与えるための指示情報

## React DOM

React DOM には（ブラウザの DOM 環境で動作する）ウェブアプリケーションでのみ用いられる機能が含まれます。以下のセクションに分かれています。

- [フック](https://ja.react.dev/reference/react-dom/hooks) - ブラウザの DOM 環境で実行されるウェブアプリケーションのためのフック
- [コンポーネント](https://ja.react.dev/reference/react-dom/components) - React がサポートする組み込みの HTML および SVG コンポーネント
- [API](https://ja.react.dev/reference/react-dom) - ウェブアプリケーションでのみ用いられる `react-dom` パッケージのメソッド
- [クライアント API](https://ja.react.dev/reference/react-dom/client) - クライアント（ブラウザ）で React コンポーネントをレンダーするための `react-dom/client` API 群
- [サーバ API](https://ja.react.dev/reference/react-dom/server) - サーバで React コンポーネントを HTML にレンダーするための `react-dom/server` API 群

## React のルール

React には、理解しやすい方法でパターンを表現し高品質なアプリケーションを産み出すための慣用的な記法、ないしルールが存在します。

- [コンポーネントとフックを純粋に保つ](https://ja.react.dev/reference/rules/components-and-hooks-must-be-pure) – これらを純粋に保つことにより、コードの理解やデバッグが容易になり、React がコンポーネントやフックを自動的に正しく最適化できるようになります。
- [コンポーネントやフックを呼び出すのは React](https://ja.react.dev/reference/rules/react-calls-components-and-hooks) – ユーザ体験を最適化するために必要に応じてコンポーネントやフックを呼び出すというのは React 自身の責務です。
- [フックのルール](https://ja.react.dev/reference/rules/rules-of-hooks) – フックは再利用可能な UI ロジックを表す JavaScript の関数として定義されており、呼び出せる場所に関する制約があります。

## レガシー API

- [レガシー API](https://ja.react.dev/reference/react/legacy) - `react` パッケージからエクスポートされているが新しいコードでは使用が推奨されないもの[Next フック](https://ja.react.dev/reference/react/hooks)

React リファレンス概要 – React