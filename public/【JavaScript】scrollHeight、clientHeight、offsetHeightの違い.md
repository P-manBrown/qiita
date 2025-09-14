---
title: 【JavaScript】scrollHeight、clientHeight、offsetHeightの違い
tags:
  - JavaScript
private: false
updated_at: '2025-09-14T23:58:54+09:00'
id: f14c33cf9b23b1f8f0b4
organization_url_name: null
slide: false
ignorePublish: false
---
## 基本的な違い

| プロパティ | 測定内容 | 含まれるもの |
|---|---|---|
| `scrollHeight` | スクロール可能な全コンテンツ高さ | パディング + 全コンテンツ（非表示部分含む） |
| `clientHeight` | 表示可能領域の高さ | パディング（ボーダー・スクロールバー除く） |
| `offsetHeight` | 要素の実際の高さ | パディング + ボーダー + スクロールバー |

## 計算式

```javascript
// 基本的な取得方法
const element = document.getElementById('target');

console.log(element.scrollHeight);  // 全コンテンツ高さ
console.log(element.clientHeight);  // 表示領域高さ  
console.log(element.offsetHeight);  // 実際の要素高さ
```

## 例

### スクロール判定（scrollHeight）

```javascript
// スクロールが最下部に到達したかを判定
function isScrolledToBottom(element) {
  return Math.abs(
    element.scrollHeight - element.clientHeight - element.scrollTop
  ) <= 1;
}
```

### オーバーフロー検出

```javascript
// コンテンツがオーバーフローしているかチェック
function isOverflowing(element) {
  return element.scrollHeight > element.clientHeight;
}
```

### レイアウト計算（offsetHeight）

```javascript
// 要素の実際のサイズを考慮した配置
function positionBelow(targetElement, referenceElement) {
  const top = referenceElement.offsetTop + referenceElement.offsetHeight;
  targetElement.style.top = top + 'px';
}
```

## 特殊なケース

### ルート要素での使用
```javascript
// ビューポートの高さを取得
const viewportHeight = document.documentElement.clientHeight;
```

### 非表示要素での注意点
```javascript
// display: noneの要素では全て0を返す
hiddenElement.offsetHeight;  // 0
hiddenElement.clientHeight;  // 0
hiddenElement.scrollHeight;  // 0
```

## 参考

https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollHeight

https://developer.mozilla.org/en-US/docs/Web/API/Element/clientHeight

https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetHeight
