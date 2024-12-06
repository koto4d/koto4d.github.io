---
title: "Scoopの使い方"
date: 2020-08-23
weight: 1
description: >
  Scoopの使い方です。

---

## Scoopとは

Scoopはコマンドラインで実行できるアプリケーション管理ツールです。
Scoopを使うとアプリケーションのインストール・アンインストール・アップデートがコマンドひとつで簡単に実行できます。
うっとうしいUACポップアップやインストールウィザードが表示されることがなくなります。

## Scoopのインストール

PowerShellを起動して，以下のコマンドを実行します。

```
Set-ExecutionPolicy RemoteSigned -scope CurrentUser -force
Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')
```

以上でインストールは終わりです。

## アプリケーションのインストールとアンインストール

Scoopを使ってアプリケーションをインストールするには `install` コマンドを使います。
例えばgitをインストールするには以下のコマンドをコマンドプロンプトで実行します。

```
scoop install git
```

逆にアンインストールする場合は `uninstall` コマンドを使います。

```
scoop uninstall git
```

## bucketの追加

Scoopで管理するアプリケーション群はbucketというまとまりごとに分けられています。
bucketの一覧は [Known application buckets](https://github.com/lukesampson/scoop#known-application-buckets) にあります。

インストール直後は `main` bucketだけが管理対象となっています。
使いたいアプリケーションが `main` 以外のbucketに入っている場合は，そのbucketを管理対象に追加しないといけません。
例えば `extras` bucketを追加したい場合は以下のコマンドを実行します。

```
scoop bucket add extras
```

これで `extras` bucketに含まれるアプリケーションも簡単にインストールできるようになります。
例えば `extras` bucketに含まれる `everything` や `heidisql` をインストールするには以下のコマンドを実行します。

```
scoop install everything heidisql
```

とりあえず `extras` bucketは追加しておいたほうが良いと思います。
Javaで開発をしている場合は `java` bucketを追加しておくと，各種JDKが簡単にインストールできます。

## Scoopのアップデート

Scoopをアップデートするには以下のコマンドを実行します。

```
scoop update
```

## アプリケーションをアップデート

Scoopでインストールしたアプリケーションをアップデートするには以下のコマンドを実行します。

```
scoop update *
```

## 参考

- [Scoop公式](https://scoop.sh/)
