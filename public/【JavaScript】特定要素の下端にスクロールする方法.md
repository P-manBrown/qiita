---
title: 【JavaScript】特定要素の下端にスクロールする方法
tags:
  - JavaScript
private: false
updated_at: '2025-11-11T23:36:08+09:00'
id: 006a1e319a64fdc8c599
organization_url_name: null
slide: false
ignorePublish: false
---
## スクロール方法

要素の下端にスクロールするには、`scrollIntoView`に`block: "end"`オプションを指定します。

```javascript
const element = document.getElementById("target");
element.scrollIntoView({ block: "end" });
```

論理値での指定も可能です。

```javascript
// 下端にスクロール
element.scrollIntoView(false);

// 上端にスクロール
element.scrollIntoView(true);
```

`false`を指定すると`{block: "end", inline: "nearest"}`と同じ動作になります。

## 参考

https://developer.mozilla.org/ja/docs/Web/API/Element/scrollIntoView
