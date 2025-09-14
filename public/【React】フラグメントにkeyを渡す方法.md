---
title: 【React】フラグメントにkeyを渡す方法
tags:
  - React
private: false
updated_at: '2025-09-13T23:51:32+09:00'
id: c417b83785c8b1cce6b3
organization_url_name: null
slide: false
ignorePublish: false
---
リスト内でフラグメントを使う際、省略記法 `<>...</>` では `key` を渡せません。

```jsx
// ❌ keyが設定できない
{items.map(item => 
  <>
    <h1>{item.title}</h1>
    <p>{item.body}</p>
  </>
)}
```

`Fragment` を明示的にインポートして使用します。

```jsx
import { Fragment } from 'react';

// ✅ keyを渡せる
{items.map(item => 
  <Fragment key={item.id}>
    <h1>{item.title}</h1>
    <p>{item.body}</p>
  </Fragment>
)}
```

## 参考

https://ja.react.dev/reference/react/Fragment#rendering-a-list-of-fragments
