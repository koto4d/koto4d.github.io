---
title: "File Browser拡張の変更"
date: 2025-02-12 14:53:51
tags: [ Visual Studio Code ]
weight: 1
description:
  
---

## "~/"を入力したときに開くフォルダを変更する

WindowsだとUSERPROFILE環境変数で設定されたフォルダが開かれてしまうのを変更します。

  1. `C:\Users\<USERNAME>\.vscode\extensions\bodil.file-browser-0.2.11\out\extension.js` を開く。
  2. 158行目`this.stepIntoFolder(path_1.Path.fromFilePath(OS.homedir()));`にある`OS.homedir()`の箇所を開きたいフォルダに変更する。
  3. ファイルを保存してvscodeを再起動する。

File Browser拡張がバージョンアップされたらまた変更が必要です。
