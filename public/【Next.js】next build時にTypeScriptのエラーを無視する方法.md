---
title: 【Next.js】next build時にTypeScriptのエラーを無視する方法
tags:
  - 'Next.js'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

## はじめに

`next build`を実行した際にTypeScriptのエラーが存在する場合、ビルドは失敗します。

TypeScriptのエラーを無視してビルドする設定について記述します。

## 設定方法

`next.config.js`に以下を追記します。

```javascript
module.exports = {
  typescript: {
    ignoreBuildErrors: true,
  },
}
```

すると`next build`実行時にTypeScriptのエラーが存在してもビルドされるようになります。

## 参考

https://nextjs.org/docs/app/api-reference/config/next-config-js/typescript
