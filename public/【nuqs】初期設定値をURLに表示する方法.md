---
title: 【nuqs】初期設定値をURLに表示する方法
tags:
  - nuqs
private: false
updated_at: '2025-07-03T23:53:39+09:00'
id: c19f6920d1aede2c1f93
organization_url_name: null
slide: false
ignorePublish: false
---
## 表示方法

初期設定値をURLに表示するには`useQueryState`のオプションとして`clearOnDefault: false`を渡します。

```jsx
useQueryState('search', {
  defaultValue: 'sample',
  clearOnDefault: false
})
```

上記のように記述することでクエリパラメーターの値が`sample`の場合でもURLに表示されます。

## 参考

https://nuqs.47ng.com/docs/options#clear-on-default
