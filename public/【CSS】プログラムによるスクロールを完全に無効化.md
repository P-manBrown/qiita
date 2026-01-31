---
title: 【CSS】プログラムによるスクロールを完全に無効化
tags:
  - 'CSS'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 概要

CSSの`overflow: clip`を使うと、通常のスクロールだけでなく、JavaScriptによるプログラマティックなスクロールも完全に無効化できます。

## overflow: clipの特徴

- はみ出したコンテンツを視覚的に隠す
- **プログラムによるスクロールを完全に無効化**
- 要素はスクロールコンテナではなくなる

## スクロール無効化の挙動

```javascript
// overflow: clipの場合
const clipElement = document.getElementById("clip");
clipElement.scrollTop = clipElement.scrollHeight; // 動作しない

// overflow: hiddenの場合（比較）
const hiddenElement = document.getElementById("hidden");
hiddenElement.scrollTop = hiddenElement.scrollHeight; // 動作する
```

`overflow: hidden`ではJavaScriptによるスクロールは可能ですが、`overflow: clip`では完全に無効化されます。

## 軸ごとの独立制御

`overflow: clip`では軸間の依存関係がありません。
```css
/* 正常動作:x軸は表示、y軸はクリップ */
.element {
  overflow-x: visible;
  overflow-y: clip;
}
```

## 参考

https://developer.mozilla.org/en-US/docs/Web/CSS/overflow#clip