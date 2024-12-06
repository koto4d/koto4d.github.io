---
title: "Git commit commentのガイドライン"
tags: [ Git ]
description: >
  Git commit commentの書き方のガイドライン。

---

## 書式

以下の書式でcommit commentを書く。

```
<type>[optional scope]: <description>

[optional body]

[optional footer]
```

## type

typeには以下を指定する。

- feat: 新しい機能
- fix: バグの修正
- imp: 機能を改善する
- change: 機能を変更する
- remove: 機能を削除
- refactor: バグ修正や新しい機能の追加以外のコードの変更。コードを整理する
- perf: 性能を改善するコードの変更
- build: ビルドシステムや外部ライブラリなどの依存に変更
- ci: CIのための設定やスクリプトの変更
- docs: ドキュメントだけの変更
- style: コードの内容に影響のない変更 (フォーマットなどの変更)
- test: 不足しているテストの追加やテストの修正
- chore: 雑多な修正

## 例

https://www.conventionalcommits.org/ja/v1.0.0-beta.4/#%E4%BE%8B から引用。

```
feat: allow provided config object to extend other configs
BREAKING CHANGE: `extends` key in config file is now used for extending other config files
chore!: drop Node 6 from testing matrix
BREAKING CHANGE: dropping Node 6 which hits end of life in April
docs: correct spelling of CHANGELOG
feat(lang): add polish language
fix: correct minor typos in code
```

## 参考

- [Conventional Commits](https://www.conventionalcommits.org/ja/v1.0.0-beta.4/)
- [Angular - Commit Message Guidelines](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines)
- [gitにおけるコミットログ/メッセージ例文集100 ](https://anond.hatelabo.jp/20160725092419)
