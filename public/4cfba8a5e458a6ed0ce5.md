---
title: 【Next.js】サーバーコンポーネントでCookieを使用する方法
tags:
  - Next.js
private: false
updated_at: '2024-02-19T02:07:27+09:00'
id: 4cfba8a5e458a6ed0ce5
organization_url_name: null
slide: false
ignorePublish: false
---
以下のように記述することでサーバーコンポーネントでCookieが使用できます。

```tsx
import { cookies } from 'next/headers'

async function getData() {
  const res = await fetch("http//sample.com", {
    method: 'GET',
    headers: {
      Cookie: cookies().toString(),
    },
    cache: 'no-cache',
  })

  if (!res.ok) {
    throw new Error('Failed to fetch data')
  }

  return res.json()
}

export default async function Sample() {
  const data = await getData()
  return (
    <div>...</div>
  )
}
```

リクエストはできますが、HTTPではストリーミング開始後にCookieを設定することができないため、レスポンスのCookieをサーバーコンポーネントでセットすることはできません。

レスポンスのCookieをセットする場合には、Middleware、Server Actions、Route Handler、のいずれかを使用する必要があります。

https://nextjs.org/docs/app/api-reference/functions/cookies#cookiessetname-value-options

サーバーコンポーネントでCookieをセットする必要がある場合には以下を参照してください。

https://github.com/vercel/next.js/discussions/49843

https://github.com/moshest/next-client-cookies

上記のライブラリは`HttpOnly`は設定できないようです。
