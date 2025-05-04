---
title: 【TypeScript】ユニオン型から指定した値を除外したユニオン型を作成する方法
tags:
  - TypeScript
private: false
updated_at: '2024-03-04T00:03:11+09:00'
id: c034e4af1a2deab0eb79
organization_url_name: null
slide: false
ignorePublish: false
---
以下のように記述するとユニオン型から指定した値のみ除外したユニオン型を作成できます。

```ts
type T1 = "A" | "B" | "C" | "D" | "E"
type T2 = Exclude<T1, "E">

// T2 = "A" | "B" | "C" | "D"
```

https://www.typescriptlang.org/docs/handbook/utility-types.html#excludeuniontype-excludedmembers
