---
title: "EmacsからVSCodeへの移行"
date: 2025-02-13 18:47:50
tags: [ Visual Studio Code, Emacs ]
weight: 1
description:
  
---

EmacsからVSCodeへの移行したときのメモです。

## キーバインド

[Awsome Emacs Keymap](https://marketplace.visualstudio.com/items?itemName=tuttieee.emacs-mcx)をインストールしました。

## find-fileっぽいもの

[File Browser](https://marketplace.visualstudio.com/items?itemName=bodil.file-browser)をインストールしました。

`~`入力時に開くフォルダを変更したいので以下のページのように修正しています。
  - [File Browser拡張](/vscode/change-file-browser)

## diredっぽいもの

[vscode-dired](https://marketplace.visualstudio.com/items?itemName=rrudi.vscode-dired)をインストールしました。

`keybindings.json`に以下の追記もしました。

``` json
    {
        "key": "ctrl+x d",
        "command": "extension.dired.open",
        "when": "editorTextFocus && !inDebugRepl"
    }
```

## emacsclient

`code -r`で代用します。

## M-x

`Ctrl-Shift-P`でコマンドを実行できます。

## 現在行の表示

`settings.json`に以下を追記しました。

``` json
    "editor.renderLineHighlight": "line",
    "workbench.colorCustomizations": {
        "editor.lineHighlightBackground": "#E8F2FE",
    },
```

## 日本語対応

日本語ファイルを開いたときに化けることがあるので`settings.json`に以下を追記しました。

``` json
    "files.autoGuessEncoding": true,
```

## 改行コード

`settings.json`に以下を追記しました。

``` json
    "files.eol": "\n",
    "files.insertFinalNewline": true,
```

## Ctrl-Tabの順序

見た目のタブ順に移動するように，`keybindings.json`に以下を追記しました。

``` json
    {
        "key": "ctrl+tab",
        "command": "workbench.action.nextEditor"
    },
    {
        "key": "ctrl+shift+tab",
        "command": "workbench.action.previousEditor"
    }    
```

## ホワイトスペースの表示

行末のホワイトスペースだけ表示するように`settings.json`に以下を追記しました。

``` json
    "editor.renderWhitespace": "trailing",
```

## 全角スペースの表示

[zenkaku](https://marketplace.visualstudio.com/items?itemName=mosapride.zenkaku)をインストールしました。
