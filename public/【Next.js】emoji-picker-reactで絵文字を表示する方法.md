---
title: 【Next.js】emoji-picker-reactで絵文字を表示する方法
tags:
  - 'Next.js'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 表示方法

以下のように記述することでemoji-piciker-reactで絵文字を表示できます。

```jsx
'use client'

import dynamic from 'next/dynamic'

const Emoji = dynamic(
  () => import('emoji-picker-react').then((mod) => mod.Emoji),
  {
    ssr: false,
  },
)

export function SampleEmoji() {
  return <Emoji unified={unified} size={24} />
}

```

## 参考

https://github.com/ealush/emoji-picker-react#nextjs
