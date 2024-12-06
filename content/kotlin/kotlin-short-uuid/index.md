---
title: "KotlinでShort UUIDを生成"
date: 2022-09-25T00:42:58
tags: [ Kotlin ]
description: >
  Kotlinでユニークかつ短い文字列の作り方。

---

## 問題

Kotlinでユニークかつ短いIDを作りたい。UUIDの文字列表現は長すぎる。


## 解決策

UUIDを生成してそれをBase64でエンコードするのがお手軽。

標準的なBase64だと `+` や `/` が使われてしまうので， `Base64.getUrlEncoder()` で取得したEncoderを使用します。
`Base64.getUrlEncoder()` で取得したEncoderは代わりに `+` や `/` の代わりに `-` と `_` を使うのでファイル名やURLに使用できます。

```kotlin
class ShortUuid {
    fun generate(): String {
        val uuid = UUID.randomUUID();
        val byteBuffer = ByteBuffer.wrap(ByteArray(16))
            .putLong(uuid.mostSignificantBits)
            .putLong(uuid.leastSignificantBits)

        return Base64.getUrlEncoder()
            .withoutPadding()
            .encodeToString(byteBuffer.array())
    }
}
```

## 参考

- [short-uuid](https://github.com/oculus42/short-uuid/blob/develop/index.js)
- [Are Base64 encoded UUIDs unique?](https://stackoverflow.com/questions/57778312/are-base64-encoded-uuids-unique)

