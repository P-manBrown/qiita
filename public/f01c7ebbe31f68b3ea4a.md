---
title: 【TypeScript】ユニオン型から指定した値のみのユニオン型を作成する方法
tags:
  - TypeScript
private: false
updated_at: '2024-03-05T00:00:04+09:00'
id: f01c7ebbe31f68b3ea4a
organization_url_name: null
slide: false
ignorePublish: false
---

以下のように記述するとユニオン型から指定した値のみのユニオン型を作成できます。

```ts
type T1 = "A" | "B" | "C" | "D" | "E"
type T2 = Extract<T1, "E">

// T2 = "E"
```

https://www.typescriptlang.org/docs/handbook/utility-types.html#extracttype-union
