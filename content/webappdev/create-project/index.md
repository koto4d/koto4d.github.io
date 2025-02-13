---
title: "Webアプリケーションプロジェクトの作成手順"
date: 2025-02-13 17:30:00
tags: [ PNPM, workspace, React Router, Prisma ]
weight: 1
description:
  
---

Webアプリケーションプロジェクト作成のおおまかな手順です。
構成は以下の通りです。

  - example-web:
    - React Routerを使ったWebアプリケーションパッケージ。
  - example-core:
    - Prismaを使ったライブラリパッケージ。

## プロジェクトの作成

ルートパッケージを作成します。

``` bash
mkdir example
cd example
pnpm init
```

## example-webパッケージの作成

example-webというReact Routerを使ったWebアプリケーションパッケージを作成します。

``` bash
mkdir typescript
cd typescript
pnpm dlx create-react-router@latest example-web # Install dependencies with pnpm?はnoを選択
```

## example-coreパッケージの作成

example-coreというライブラリパッケージを作成します。

``` bash
cd /path/to/example/typescript
mkdir example-core
pnpm init
```

## pnpm workspaceの設定

`example/pnpm-workspace.yaml`ファイルを作成して以下の内容を記述します。

``` yaml  
packages:
  - 'typescript/*'
```

以下のコマンドを実行します。

``` bash
cd /path/to/example
pnpm i
pnpm approve-builds
```

## example-coreにTypeScript，Prismaをインストール

以下のコマンドを実行します。

``` bash
pnpm --filter example-core i prisma typescript tsx @types/node --save-dev
pnpm --filter example-core exec tsc --init
pnpm --filter example-core exec prisma
pnpm --filter example-core exec prisma init
pnpm approve-builds
```

## example-webパッケージからexample-coreパッケージへのdependencyを追加

`example-web/package.json`に以下の依存を追加します。

``` json
    "example-core": "workspace:1.0.0",
```

以下を実行します。

``` bash
cd /path/to/example
pnpm i
```
