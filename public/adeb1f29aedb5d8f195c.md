---
title: 【TypeScript】型の条件分岐
tags:
  - TypeScript
private: false
updated_at: '2023-11-18T13:35:22+09:00'
id: adeb1f29aedb5d8f195c
organization_url_name: null
slide: false
ignorePublish: false
---
以下のように記述すると`id`と`name`は`isLoading`が`true`の場合には任意に`false`の場合には必須になります。

```ts
type Sample<T extends boolean> = T extends true
  ? {
      isLoading: T
      id?: string
      name?: string
    }
  : {
      isLoading: T
      id: string
      name: string
    }


// 以下のように使用
Sample<boolean>
```

`Sample<boolean>`のように引数に`boolean`を設定した場合には`Sample<true | false>`とした場合と同様になります。
結果として以下のような型になります。

```ts
type SampleBoolean = Sample<boolean>

type SampleBoolean =
  | {
      isLoading: true
      id?: string
      name?: string
    }
  | {
      isLoading: false
      id: string
      name: string
    }
```

https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#distributive-conditional-types

そのため、`id`と`name`は`isLoading`が`true`の場合には任意に、`false`の場合には必須ということになります。

また、`Sample`の引数に`boolean`ではなく`true`、`false`というより具体的な型を指定すると以下のようになります。

```ts
type SampleTrue = Sample<true>

type SampleTrue = 
  {
    isLoading: true
    id?: string
    name?: string
  }


type SampleFalse = Sample<false>

type SampleFalse = 
  {
    isLoading: false
    id: string
    name: string
  }
```
