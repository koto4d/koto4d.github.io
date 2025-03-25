---
title: "TypeScriptによるWebアプリケーション開発の技術スタック"
date: 2025-03-25 19:19:18
tags: [ PNPM, React Router, Drizzle ORM, TSUP, PostgreSQL, Docker, AWS, RDS, ECS, CDK ]
weight: 1
description:
  
---

TypeScriptによるWebアプリケーションの開発で利用できる技術スタックについて説明します。
TypeScriptでできることはTypeScriptでする，というポリシーで選定しています。

### パッケージマネージャ

npm，yarn，pnpmなどありますが，pnpmを使用します。
npmに近い使い勝手で，高速に動作し，ディスク効率もよいことからpnpmを選択します。
システムを複数のパッケージに分割して構成するためのworkspace機能についても対応しています。

- https://pnpm.io/ja/

### Webフレームワーク

React Router (フレームワークモード)を使用します。
ルーティングを管理でき，SSRやCSRの実装がシンプルにでき，パフォーマンスがよいことからReact Routerを選択します。

- https://reactrouter.com/

### バンドラ

React Routerから使用されるパッケージ用のバンドラにはtsupを使用します。
非常に少ない設定でTypeScriptのコードを他のパッケージから利用可能な形にバンドルできます。

- https://tsup.egoist.dev/

### ORM

ORMにはDrizzle ORMを使用します。
TypeScriptで型安全なクエリを記述することができます。
性能もPrismaに比べてよいです。

- https://orm.drizzle.team/

### DB

PostgreSQLを使用します。
Drizzle ORMから利用でき，性能もよいです。
MySQLの方がなれているのであればそちらでもよいと思います。

- https://www.postgresql.org/

### コンテナ

Dockerを使用します。
デプロイ先ことであまり悩まないようにコンテナ化してデプロイします。

- https://www.docker.com/ja-jp/

### インフラ

AWSのECSやRDSなどを使用します。
コンテナ化したWebアプリケーションをECSにデプロイします。
DBはAWS RDSを使用します。

- https://aws.amazon.com/jp

### IaC

CDK (TypeScript)を使用します。
AWSのインフラをTypeScriptのコードで管理できます。

- https://aws.amazon.com/jp/cdk/

以上
