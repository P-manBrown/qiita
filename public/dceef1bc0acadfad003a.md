---
title: '【Next.js】ReferenceError: window is not defined解消法'
tags:
  - Next.js
private: false
updated_at: '2023-10-11T23:57:18+09:00'
id: dceef1bc0acadfad003a
organization_url_name: null
slide: false
ignorePublish: false
---
`ReferenceError: window is not defined`のエラーが発生した場合には以下のように記述することで解消できます。

```tsx
import { useEffect } from 'react'

export default function Sample() {
  useEffect(() => {
    // windowが必要な処理
  }, [])

  return (
    
  )
}

```
