---
title: 【JavaScript】マウスホイールのスクロール量を取得する方法
tags:
  - JavaScript
private: false
updated_at: '2025-11-03T23:51:22+09:00'
id: a307ba4157fd0c11ddf6
organization_url_name: null
slide: false
ignorePublish: false
---
## 取得方法

```javascript
element.addEventListener('wheel', (event) => {
  console.log('横方向:', event.deltaX);
  console.log('縦方向:', event.deltaY);
  console.log('Z軸方向:', event.deltaZ);
  console.log('単位:', event.deltaMode);
});
```

### deltaX / deltaY / deltaZ

スクロール量を表す`double`型の値です。

- `deltaX`: 横方向のスクロール量
- `deltaY`: 縦方向のスクロール量
- `deltaZ`: Z軸方向のスクロール量

### deltaMode

`delta*`値の単位を表す`unsigned long`型の値です。

- `0` (DOM_DELTA_PIXEL): ピクセル単位
- `1` (DOM_DELTA_LINE): 行単位
- `2` (DOM_DELTA_PAGE): ページ単位

## 例

```javascript
const container = document.getElementById('container');

container.addEventListener('wheel', (event) => {
  // デフォルトのスクロールを防止
  event.preventDefault();
  
  // スクロール量に応じた処理
  if (event.deltaY > 0) {
    console.log('下にスクロール');
  } else if (event.deltaY < 0) {
    console.log('上にスクロール');
  }
  
  // 単位に応じた処理
  const pixelAmount = event.deltaMode === 0 
    ? event.deltaY 
    : event.deltaY * 16; // 行単位の場合は概算でピクセルに変換
    
  console.log(`スクロール量: ${pixelAmount}px`);
});
```

## 参考

https://developer.mozilla.org/en-US/docs/Web/API/WheelEvent
