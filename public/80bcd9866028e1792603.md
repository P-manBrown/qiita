---
title: 【Next.js】Linkで動的ルートの完全なルートをプリフェッチする方法
tags:
  - Next.js
private: false
updated_at: '2025-08-04T23:49:41+09:00'
id: 80bcd9866028e1792603
organization_url_name: null
slide: false
ignorePublish: false
---
以下のように`prefetch={true}`を記述すると動的ルートでも完全なルートがプリフェッチされます。

```jsx
<Link href="/sample" prefetch={true}}>サンプル</Link>
```
