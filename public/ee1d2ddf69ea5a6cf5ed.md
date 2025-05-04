---
title: 【JavaScript】URL.canParse()の使い方
tags:
  - JavaScript
private: false
updated_at: '2024-10-26T23:45:27+09:00'
id: ee1d2ddf69ea5a6cf5ed
organization_url_name: null
slide: false
ignorePublish: false
---
## `URL.canParse()`を使用する

`URL.canParse()`の引数にURL文字列を渡すことで有効か判定できます。

```js
function isValidURL(url) {
  return URL.canParse(url)
}
```

https://developer.mozilla.org/ja/docs/Web/API/URL/canParse_static

## URLの有効性を判定する他の方法

`URL()`コンストラクターが与えられたURL文字列が有効でなければ例外をスローすることを利用して以下のように判定することもできます。

```js
function isValidURL(url) {
  try {
    new URL(url)
    return true
  } catch {
    return false
  }
}
```

https://developer.mozilla.org/ja/docs/Web/API/URL/URL

## 参考

https://developer.mozilla.org/ja/docs/Web/API/URL#%E4%BD%BF%E7%94%A8%E4%B8%8A%E3%81%AE%E6%B3%A8%E6%84%8F
