---
title: 【Next.js】Linkコンポーネントで遷移する際に処理を実行する方法
tags:
  - Next.js
private: false
updated_at: '2025-06-23T23:58:40+09:00'
id: 9862da73e538681762a8
organization_url_name: null
slide: false
ignorePublish: false
---
## 方法

`Link`コンポーネントの`onNavigate`に関数を渡すことで遷移する際に処理を実行できます。

```tsx
import Link from 'next/link'
 
export default function Page() {
  return (
    <Link
      href="/sample"
      onNavigate={() => {
        console.log('Navigating...')
      }}
    >
      サンプル
    </Link>
  )
}
```

`preventDefault()`を実行すると遷移をキャンセルできます。

```tsx
import Link from 'next/link'
 
export default function Page() {
  return (
    <Link
      href="/sample"
      onNavigate={(e) => {
        e.preventDefault()
      }}
    >
      サンプル
    </Link>
  )
}
```

## 参考

https://nextjs.org/docs/app/api-reference/components/link#onnavigate
