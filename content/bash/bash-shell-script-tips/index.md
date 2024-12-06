---
title: "Bash Shell Script Tips"
tags: [ Bash, Shell Script ]
description: >
  Bash Shell ScriptのTips。

---

## 文字列を含むか判定

ある文字列にある文字列が含まれるかを判定するには以下のように `if` を記述します。

```sh
STR='GNU/Linux is an operating system'
SUB='Linux'
if [[ "$STR" == *"$SUB"* ]]; then
  echo "It's there."
fi
```
## OSの判定

OSを判定するには `uname` コマンドを使います。

```sh
if [[ "$(uname)" == *'Linux'* ]]; then
    echo "linux"
elif [[ "$(uname)" == *'Darwin* ]]; then
    echo "mac"
elif [[ "$(uname)" == *'MINGW64'* ]]; then
    echo "win"
fi
```

## 変数の空文字判定

変数が空文字かを判定するには以下のように `if` を記述します。
変数を""で囲む必要があることに注意。

STRING変数が空または空文字でないかどうか。

```bash
if [ -n "$STRING" ]; then
  # 空でないときの処理
fi
```

STRING変数が空または空文字かどうか。

```bash
if [ -z "$STRING" ]; then
  # 空のときの処理
fi
```

## 変数の大文字化/小文字化

変数の大文字化または小文字化。

| 記述     | 説明                    | 例                             |
| -------- | ---------------------- | ------------------------------ |
| `${v^}`  | 大文字化(１文字目のみ)  | `v="ho ge"; echo ${v^}`→Ho ge  |
| `${v^^}` | 大文字化(全文字)        | `v="ho ge"; echo ${v^^}`→HO GE |
| `${v,}`  | 小文字化(１文字目のみ)  | `v="HO GE"; echo ${v,}`→hO GE  |
| `${v,,}` | 小文字化(全文字)        | `v="HO GE"; echo ${v,,}`→ho ge |
| `${v~}`  | 大小反転(１文字目のみ※) | `v="ho GE"; echo ${v~}`→Ho gE  |
| `${v~~}` | 大小反転(全文字)        | `v="ho GE"; echo ${v~~}`→HO GE |

## コマンド補完時に大文字小文字を区別しない

`.inputrc` に以下を追加します。

```
set completion-ignore-case on
```
