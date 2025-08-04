---
title: 【Next.js】Linkで動的ルートの完全なルートをプリフェッチする方法
tags:
  - ''
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
以下のように`prefetch={true}`を記述すると動的ルートでも完全なルートがプリフェッチされます。

```jsx
<Link href="/sample" prefetch={true}}>サンプル</Link>
```
