---
title: 【Next.js】error.tsxでデータ取得を再試行する方法
tags:
  - Next.js
private: false
updated_at: '2025-10-03T23:37:46+09:00'
id: 9807162c5945fb459014
organization_url_name: null
slide: false
ignorePublish: false
---
## 問題：reset()だけでは動作しない

`error.tsx`で`reset()`を実行しても、サーバー側のコードが再実行されず、データの再取得が行われません。

```tsx
'use client'

export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string }
  reset: () => void
}) {
  return (
    <div>
      <h2>エラーが発生しました</h2>
      <button onClick={() => reset()}>
        再試行
      </button>
    </div>
  )
}
```

## 解決策：router.refresh()とstartTransitionを組み合わせる

`reset()`に加えて`router.refresh()`を`startTransition`でラップすることで、サーバー側のデータ取得を再実行できます。

```tsx
'use client'

import { useRouter } from 'next/navigation'
import { startTransition } from 'react'

export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string }
  reset: () => void
}) {
  const router = useRouter()

  function handleRetry() {
    startTransition(() => {
      router.refresh() // サーバー側のデータを再取得
      reset()          // error boundaryをリセット
    })
  }

  return (
    <div>
      <h2>エラーが発生しました</h2>
      <button onClick={handleRetry}>
        再試行
      </button>
    </div>
  )
}
```

## なぜこの方法で動作するのか

### router.refresh()の役割
- サーバー側でルートを再実行
- データ取得ロジックとServer Componentsを再レンダリング
- 新しいデータをクライアントに送信

### reset()の役割
- error boundary 内のコンポーネントを再レンダリング

### startTransition()の役割
- 重い処理をノンブロッキングで実行
- クライアントサイドとサーバーサイドの両コンポーネントを同時に再レンダリング

この3つを組み合わせることで、サーバー側のデータを再取得しつつ、error boundary を適切にリセットできます。

## 参考

https://github.com/vercel/next.js/issues/63369#issuecomment-2211698627

https://dopoto.github.io/blog/20250228-nextjs-reset
