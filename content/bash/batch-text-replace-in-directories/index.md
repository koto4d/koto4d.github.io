---
title: "複数のファイル内の文字列を一括置換"
date: 2020-09-03T00:00:00+09:00
tags: [ bash ]
description: >
  複数のファイル内の文字列を一括置換するコマンドの例。

---

## 例1

```
find . -type f -name "kustomization*" | grep base/ | xargs sed -i -e 's/deployment/resources/g'
```
- 対象: カレントディレクトリ以下 (サブディレクトリ下含む) にあるファイル & ファイル名が `kustomization` で始まる & パスに `base/` を含む
- 置換: ファイル内の `deployment` という文字列を `resources` に置換


## 例2

```
find . -type f -name "*.config" -print0 | xargs grep -l foo | xargs sed -i "s/yaml/yml/g"
```

- 対象: カレントディレクトリ以下 (サブディレクトリ下含む)にあるファイル & 拡張子が `.config` & ファイル内に `foo` という文字列を含むファイル
- 置換: `yaml` という文字列を `yml` に置換
