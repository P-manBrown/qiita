---
title: 【Next.js】Dynamic Import を使用してSSRしないようにする方法
tags:
  - Next.js
private: false
updated_at: '2024-04-19T00:00:33+09:00'
id: 2762caa7ea4b2c1efdbb
organization_url_name: null
slide: false
ignorePublish: false
---
以下のようにDynamic Inportの際に　`{ssr: false}` を第二引数に渡すとSSRされず、React単体のようにクライアントでのみレンダリングされます。

```jsx
import dynamic from 'next/dynamic'
 
const Sample = dynamic(
  () => import('../components/Sample'),
  {
    ssr: false,
  }
)
 
export default function Page() {
  return (
    <div>
      <Sample />
    </div>
  )
}

```
