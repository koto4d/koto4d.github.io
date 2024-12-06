---
title: "Docsyで最終更新の表示を変更"
date: 2020-08-22
description: >
  Docsyテーマを使っていて `enableGitInfo = true` としているときに，ページ下部に表示される最終更新の日付の表示を変更する方法です。

---

## config.tomlの編集

まず日付のフォーマットを指定します。

日付のフォーマットは `config.toml` の `params.time_format_default` で指定します。
指定方法は以下のとおりです。

- 年は `2006` (4桁で表示) または `06` (下2桁で表示)
- 月は `01` (2桁になるように0で埋める) または `1` (0で埋めない)
- 日は `02` (2桁になるように0で埋める) または `2` (0で埋めない)

例えば `2020-08-22` という形式で表示したいときは以下のように指定します。

```toml
[params]
  time_format_default = "2006-01-02"
```

`2020年8月22日` という形式で表示したいときは以下のように指定します。

```toml
[params]
  time_format_default = "2006年1月2日"
```

## page-meta-lastmod.htmlの作成

`layouts/partials/page-meta-lastmod.html` というファイルを作成して表示したい内容を記述します。
例えば `最終更新 2020-08-22` と表示したい場合は以下のように記述します。

```html
{{ T "post_last_mod"}} {{ .Lastmod.Format .Site.Params.time_format_default }}
```

ちなみにDocsyテーマでのもともとの定義は以下のとおりで，
`最終更新 2020-08-22: コード例を修正 (53670a5)` といった表示になります。

```html
{{ T "post_last_mod"}} {{ .Lastmod.Format .Site.Params.time_format_default }}{{ with .GitInfo }}: <a  href="{{ $.Site.Params.github_repo }}/commit/{{ .Hash }}">{{ .Subject }} ({{ .AbbreviatedHash }})</a>{{end }}
```

私は後半部分のGitHubへのリンクを張りたくないのでばっさり削除しました。


以上
