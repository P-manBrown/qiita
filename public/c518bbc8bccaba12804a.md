---
title: 【JavaScript】window.open()でnoopenerやnoreferrerを設定する方法
tags:
  - JavaScript
private: false
updated_at: '2024-10-29T23:55:37+09:00'
id: c518bbc8bccaba12804a
organization_url_name: null
slide: false
ignorePublish: false
---
以下のように記述することで`window.open()`に`noopener`と`noreferrer`を設定できます。

```js
window.open("http://example.com", "_blank", "noreferrer")
```

`noreferrer`しか記述していませんが自動的に`noopener`も適用されます。

https://developer.mozilla.org/ja/docs/Web/API/Window/open#noreferrer
