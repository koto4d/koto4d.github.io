---
title: "ChromebookでHugoを使う"
date: 2020-09-01T00:00:21+09:00
description: >
  ChromebookのLinux上でHugoを使う方法を説明します。

---

## 前提

Hugoの一般的な設定方法や使い方については [Hugo]({{< ref "/hugo" >}}) を参照してください。


## ローカル起動とChromeでの表示

ChromebookのLinuxの仕組みのため，`hugo server`で起動しても，
Chromeから http://localhost:1313 でうまくアクセスできません。

Hugoをローカル起動するには以下のコマンドを実行します。

```
hugo server --bind="0.0.0.0" --baseURL="http://penguin.linux.test"
```

Chromeで表示するには `http://penguin.linux.test` にアクセスします。

以上
