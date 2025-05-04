---
title: 【TypeScript】nullやundefinedの可能性があってもエラーが発生しないようにする
tags:
  - TypeScript
private: false
updated_at: '2024-07-26T23:57:00+09:00'
id: 7e12ecba46b3de3bb7f3
organization_url_name: null
slide: false
ignorePublish: false
---

非nullアサーション演算子(`!`)を使用すると`null`または`undefined`でないことをTypeScriptに伝えることができます。

```ts
let sample: string | null = fetchSomeNullableString()
let test: string = sample! // 非nullアサーション演算子を使用
```

上記の例では、`sample`の型は`string | null`ですが、非nullアサーション演算子を使用することで、`string`型である`test`に`sample`を代入できています。

