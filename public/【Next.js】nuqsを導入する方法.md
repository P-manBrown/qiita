---
title: 【Next.js】nuqsを導入する方法
tags:
  - 'Next.js'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## nuqsとは

nuqsは状態をクエリパラメータで管理するためのライブラリです。

https://nuqs.47ng.com/

## インストール

Yarnを使用している場合、以下のコマンドを実行してインストールします。

```terminal
yarn add nuqs
```

https://nuqs.47ng.com/docs/installation

## アダプタ

Next.jsのApp Routerを使用する場合には`RootLayout`の`{children}`を`NuqsAdapter`コンポーネントでラップします。

```tsx
import { NuqsAdapter } from 'nuqs/adapters/next/app'
import { type ReactNode } from 'react'
 
export default function RootLayout({
  children
}: {
  children: ReactNode
}) {
  return (
    <html>
      <body>
        <NuqsAdapter>{children}</NuqsAdapter>
      </body>
    </html>
  )
}

```

https://nuqs.47ng.com/docs/adapters

## 使い方

以下のように記述することでカウントをクエリパラメータで管理できるようになります。

```tsx
"use client"

import { useQueryState } from "nuqs"

export function Demo() {
  const [count, setCount] = useQueryState(
    "count",
    parseAsInteger.withDefault(0),
  )
  return (
		<button onClick={() => setCount((c) => c + 1)}>Count: {count}</button>
  )
}

```
