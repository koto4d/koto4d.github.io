---
title: "Next.jsの開発モードでRecoilのエラーが表示されないようにする"
date: 2022-09-24T02:15:25+09:00
tags: [ Next.js, Recoil ]
description: >
  Next.jsの開発モードでRecoilがエラーを出力するのを表示されなくする方法。

---

## 概要

Next.jsでRecoilを使って `npm run dev` すると以下の警告が表示される。

```
Expectation Violation: Duplicate atom key "xxx". This is a FATAL ERROR in
      production. But it is safe to ignore this warning if it occurred because of
      hot module replacement.
```

無視しても問題ないが，他の出力が見えなくなってしまって邪魔になる。

## 非表示にする方法

### next-intercept-stdoutをインストール
[next-intercept-stdout](https://www.npmjs.com/package/next-intercept-stdout) をインストールする。

```
cd path/to/your_nextjs_project
npm i next-intercept-stdout
```

### next.config.jsを編集


```
const withInterceptStdout = require('next-intercept-stdout');

module.exports = withInterceptStdout(
  {
    reactStrictMode: true,
    // your configs...
  },
  (text) => (text.includes('Duplicate atom key') ? '' : text),
);

```

これで `npm run dev` してもRecoilの警告は表示されなくなる。

以上
