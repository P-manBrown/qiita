---
title: 【Next.js】useRouterのonInvalidateの使い方
tags:
  - 'Next.js'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## onInvalidateとは

`onInvalidate`は`router.prefetch()`の第2引数として渡すコールバック関数で、プリフェッチされたデータがNext.jsによって「古い」と判断されたときに呼び出されます。

**重要な特性:**
- プリフェッチリクエストごとに**最大1回のみ**呼び出される
- キャッシュの無効化を検知し、新しいプリフェッチをトリガーするタイミングを知らせる

## 例

`onInvalidate`を使用して、キャッシュが無効化されるたびに自動的に再プリフェッチするリンクは以下のように実装できます。

```tsx
'use client'
import { useRouter } from 'next/navigation'
import { useEffect } from 'react'

function ManualPrefetchLink({
  href,
  children,
}: {
  href: string
  children: React.ReactNode
}) {
  const router = useRouter()

  useEffect(() => {
    let cancelled = false

    const poll = () => {
      if (!cancelled) {
        router.prefetch(href, { onInvalidate: poll })
      }
    }

    poll() // 初回プリフェッチを実行

    return () => {
      cancelled = true // クリーンアップ
    }
  }, [href, router])

  return (
    <a
      href={href}
      onClick={(event) => {
        event.preventDefault()
        router.push(href)
      }}
    >
      {children}
    </a>
  )
}
```

## 参考

https://nextjs.org/docs/app/api-reference/functions/use-router

https://nextjs.org/docs/app/guides/prefetching#extending-or-ejecting-link
