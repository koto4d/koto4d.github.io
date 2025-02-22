---
title: "React Routerアプリ開発での環境変数の扱い方"
date: 2025-02-22 23:03:52
tags: [ React Router, dotenv, Docker, PNPM ]
weight: 1
description: >
  
---

React Routerアプリを開発していて、開発時とリリース時のアプリに渡す環境変数の扱いについて困りました。
調べて対処法を考えたので書いておきます。

## 利用したもの

以下の3つを利用しました。

  1. React Routerの.env読み込み機能
     - React Routerにはローカル開発時に.envファイルを読み込む機能があります。
     - 参考: [環境変数](https://remix-docs-ja.techtalk.jp/guides/envvars) (Remixの文書ですがReact Routerも同様だと思います)
  2. dotenv-cli npmパッケージ
     - dotenv-cliを使うとファイルから環境変数を読み込んでコマンドに渡すことができます。
     - 参考: [dotenv-cli](https://www.npmjs.com/package/dotenv-cli)
  3. docker runの-env-file引数
     - `docker run` コマンドには `-env-file` 引数でファイルから環境変数を読み込ませられます。
     - 参考: [環境変数の設定（-e、--env、--env-file）](https://docs.docker.jp/engine/reference/commandline/run.html#e-env-env-file)

## 環境変数ファイル構成

以下の3つの環境変数定義ファイルを用意します。すべて中身は `<環境変数名>=<環境変数値>` の形式です。

  - `.env` <br>
    ローカル開発時に必要なすべての環境変数を設定します。
  - `.env.production` <br>
    リリースビルドをローカル実行するときの環境変数を設定します。.envからの差分のみを記述します。
  - `.env.docker` <br>
    リリースビルドをdockerで実行するときの環境変数を設定します。.envからの差分のみを記述します。

## ローカル開発時

ローカル開発時に必要な環境変数は `.env` に記載します。

以下の `package.json` で `pnpm build` すると読み込んでくれます。

```json
  "scripts": {
    "dev": "react-router dev",
  }
```

## リリースビルド時

### リリースビルドをローカルで実行

以下の `package.json` で `pnpm start:local` すると `.env` と `.env.production` を読み込んでくれます。

```json
  "scripts": {
    "build": "react-router build",
    "start:local": "dotenv -e .env.production -e .env -- react-router-serve ./build/server/index.js",
  }
```

dotenv-cliは指定順で先勝ちなので、`.env.production` を先に指定します。

### リリースビルドをdockerコンテナ上で実行

以下の `package.json` で `pnpm docker:run` すると `.env` と `.env.docker` を読み込んでくれます。

```json
  "scripts": {
    "docker:build": "docker build -t quilt/quilt-web .",
    "docker:run": "docker run -it -p 3000:3000 --env-file=.env --env-file=.env.docker quilt/quilt-web",
  }
```

`--env-file` 引数は後勝ちなので、`.env.docker` を後に指定します。

### リリースビルドを本番環境で実行

本番環境のやり方で環境変数を設定します。

以上

