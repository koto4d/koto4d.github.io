---
title: "複数のbashプロセスでhistoryを共有"
date: 2022-09-25T10:17:14
tags: [ bash ]

---

複数のbashプロセスでhistoryを共有するには `.bashrc` に以下の設定を記述します。

```
PROMPT_COMMAND="history -a; history -c; history -r; $PROMPT_COMMAND"
shopt -u histappend
```

一行目で，コマンドを実行するたびに以下の処理を実行します。
- コマンド履歴をhistoryファイルに追記
- メモリ上のコマンド履歴を消去
- コマンド履歴をhistoryファイルから読み込み

二行目ではbashを終了したときにコマンド履歴をhistoryファイルに書き込まないように指定しています。
