---
title: 【CSS】overflowのhiddenとclipの違い
tags:
  - CSS
private: false
updated_at: '2025-09-20T23:57:42+09:00'
id: b694e7693a3db9ea3f65
organization_url_name: null
slide: false
ignorePublish: false
---
## `overflow: hidden`

- はみ出したコンテンツを視覚的に隠す
- **プログラムによるスクロールが可能**
- 要素は依然として「スクロールコンテナ」として機能

## `overflow: clip`

- はみ出したコンテンツを視覚的に隠す
- **プログラムによるスクロールを完全に無効化**
- 要素はスクロールコンテナではなくなる

## プログラム的スクロールの動作例

```javascript
// overflow: hiddenの場合
const hiddenElement = document.getElementById("hidden");
hiddenElement.scrollTop = hiddenElement.scrollHeight; // 動作する

// overflow: clipの場合
const clipElement = document.getElementById("clip");
clipElement.scrollTop = clipElement.scrollHeight; // 動作しない
```

## 軸ごとの制御における違い

`overflow: hidden`では、軸ごとに異なる値を設定する際に制限があります。

```css
/* 問題：x軸のvisibleが無効になる */
.element {
  overflow-x: visible;
  overflow-y: hidden;
}
```

一方、`overflow: clip`では軸間の依存関係がありません。

```css
/* 正常動作：x軸は表示、y軸はクリップ */
.element {
  overflow-x: visible;
  overflow-y: clip;
}
```
