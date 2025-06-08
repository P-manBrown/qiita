---
title: 【React】状態をローカルストレージに保存する方法
tags:
  - React
private: false
updated_at: '2025-06-08T23:55:24+09:00'
id: d543556585ef48d52db9
organization_url_name: null
slide: false
ignorePublish: false
---

以下のように記述すると状態をローカルストレージに保存できます。

これにより、画面を更新するなどしても状態が維持されます。

```javascript
import React, { useState, useEffect } from 'react';

function CounterApp() {
  // ローカルストレージから初期値を取得して状態を設定
  const [count, setCount] = useState(() => {
    const savedCount = localStorage.getItem('count');
    return savedCount ? parseInt(savedCount, 10) : 0; // デフォルト値は0
  });

  // 状態が変更されるたびにローカルストレージへ保存
  useEffect(() => {
    localStorage.setItem('count', count);
  }, [count]);

  // カウントを増減させる関数
  const increment = () => setCount(count + 1);
  const decrement = () => setCount(count - 1);

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
    </div>
  );
}

export default CounterApp;
```

