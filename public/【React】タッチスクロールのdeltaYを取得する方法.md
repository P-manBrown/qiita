---
title: 【React】タッチスクロールのdeltaYを取得する方法
tags:
  - React
private: false
updated_at: '2025-11-02T21:58:21+09:00'
id: be598a2b4055cc2600a4
organization_url_name: null
slide: false
ignorePublish: false
---
## 計算方法

### タッチ開始位置を記録

```javascript
const [touchStartY, setTouchStartY] = useState(null);

const handleTouchStart = (e) => {
  const touch = e.touches[0];
  setTouchStartY(touch.clientY);
};
```

`e.touches[0]`で最初のタッチポイントを取得し、その`clientY`（Y座標）を保存します。

###  タッチ移動中にdeltaYを計算

```javascript
const handleTouchMove = (e) => {
  if (!touchStartY) return;
  
  const touch = e.touches[0];
  const currentY = touch.clientY;
  const deltaY = currentY - touchStartY;
  
  console.log(`deltaY: ${deltaY}px`);
  
  // スクロール方向の判定
  if (deltaY < 0) {
    console.log(`上方向に${Math.abs(deltaY)}pxスクロール`);
  } else if (deltaY > 0) {
    console.log(`下方向に${deltaY}pxスクロール`);
  }
};
```

### タッチ終了時にリセット

```javascript
const handleTouchEnd = () => {
  setTouchStartY(null);
};
```

## 例

### スクロール量に応じた処理

```javascript
const handleTouchMove = (e) => {
  if (!touchStartY) return;
  
  const touch = e.touches[0];
  const deltaY = touch.clientY - touchStartY;
  
  // 一定以上のスクロールで処理を実行
  if (deltaY < -50) {
    // 上方向に50px以上スクロールした場合
    loadMoreContent();
  } else if (deltaY > 50) {
    // 下方向に50px以上スクロールした場合
    refreshContent();
  }
};
```

### スクロール量の表示

```javascript
import { useState, useRef } from 'react';

function ScrollComponent() {
  const [touchStartY, setTouchStartY] = useState(null);
  const [scrollAmount, setScrollAmount] = useState(0);

  const handleTouchStart = (e) => {
    setTouchStartY(e.touches[0].clientY);
  };

  const handleTouchMove = (e) => {
    if (!touchStartY) return;
    
    const deltaY = e.touches[0].clientY - touchStartY;
    setScrollAmount(deltaY);
  };

  const handleTouchEnd = () => {
    setTouchStartY(null);
    setScrollAmount(0);
  };

  return (
    <div
      onTouchStart={handleTouchStart}
      onTouchMove={handleTouchMove}
      onTouchEnd={handleTouchEnd}
      style={{ height: '100vh', overflow: 'auto' }}
    >
      <p>スクロール量: {scrollAmount}px</p>
      {/* コンテンツ */}
    </div>
  );
}
```
