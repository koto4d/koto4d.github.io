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

## example-coreにTypeScript，TSUP，Prismaをインストール

以下のコマンドを実行します。

``` bash
pnpm --filter example-core i prisma typescript tsx @types/node tsup --save-dev
pnpm --filter example-core exec tsc --init
pnpm --filter example-core exec prisma
pnpm --filter example-core exec prisma init
pnpm approve-builds
```

`example-core/package.json`に以下を追記します。

``` json
  "type": "module",
  "main": "./dist/index.js",
  "types": "./dist/index.d.ts",
  "exports": {
    ".": {
      "import": {
        "types": "./dist/index.d.ts",
        "default": "./dist/index.js"
      }
    }
  },
  "scripts": {
    "build": "tsup",
    "build:watch": "tsup --watch",
    "db:generate": "prisma generate",
    "db:migrate": "prisma migrate dev",
    "db:migrate:reset": "prisma migrate reset --force",
    "db:seed": "prisma db seed"
  },
  "tsup": {
    "target": "es2022",
    "dts": true,
    "clean": true,
    "format": ["cjs", "esm"],
    "entryPoints": [
      "./src/index.ts"
    ]
  },
  "prisma": {
    "seed": "tsx prisma/seeds.ts"
  },
```

`example-core/tsconfig.json`を以下のように編集します。

``` json
{
  "compilerOptions": {
    "lib": ["ES2022"],
    "moduleResolution": "Bundler",
    "module": "ESNext",
    "target": "ES2022",
    "strict": true,
    "skipLibCheck": true,
    "declaration": true,
    "outDir": "./dist"
  },
  "include": ["src/**/*.ts"]
}
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

## サブプロジェクトのscriptを実行しやすくするために`package.json`を編集

`example/package.json`に以下を追記します。

``` json
  "scripts": {
    "core": "pnpm -F \"example-core\"",
    "web": "pnpm -F \"example-web\""
  },
```
