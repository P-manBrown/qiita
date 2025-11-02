---
title: 【React】progressの使い方
tags:
  - React
private: false
updated_at: '2025-11-01T23:49:08+09:00'
id: cd2d520a2d99419381ce
organization_url_name: null
slide: false
ignorePublish: false
---
## 基本的な使い方

`<progress>`コンポーネントを使用するとプログレスバーを表示できます。

```jsx
<progress value={0.5} />
```

## Props

`<progress>`コンポーネントは以下のpropsをサポートしています。

- **value**: `0`から`max`までの数値、または不確定状態の場合は`null`。完了度を指定
- **max**: 最大値を指定する数値。デフォルトは`1`

## 例

### 基本的なプログレスバー

```jsx
export default function App() {
  return (
    <>
      {/* 0% */}
      <progress value={0} />
      
      {/* 50% */}
      <progress value={0.5} />
      
      {/* 70% */}
      <progress value={0.7} />
      
      {/* 75% (maxを100に設定) */}
      <progress value={75} max={100} />
      
      {/* 100% */}
      <progress value={1} />
      
      {/* 不確定状態 */}
      <progress value={null} />
    </>
  );
}
```

### 動的なプログレスバー

```jsx
import { useState } from 'react';

export default function ProgressExample() {
  const [progress, setProgress] = useState(0);

  const handleClick = () => {
    setProgress(prev => Math.min(prev + 0.1, 1));
  };

  return (
    <div>
      <progress value={progress} />
      <p>{Math.round(progress * 100)}%</p>
      <button onClick={handleClick}>進める</button>
    </div>
  );
}
```

## 参考

https://react.dev/reference/react-dom/components/progress
