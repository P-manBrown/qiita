---
title: 【Next.js】ServerActionsのリクエストボティの最大サイズを設定する方法
tags:
  - 'nextjs'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

## デフォルトの最大サイズは1MB

ServerActionsのリクエストの最大サイズはデフォルトでは1MBとなっています。
1MBを超過すると以下のようなエラーとなります。

```terminal
 ⨯ uncaughtException: [Error: Body exceeded 1 MB limit.
                To configure the body size limit for Server Actions, see: https://nextjs.org/docs/app/api-reference/next-config-js/serverActions#bodysizelimit] {
  statusCode: 413
}
```

## 最大サイズを設定する

任意のサイズに変更するには`next.config.js`に次の設定を追記します。

```javascript
/** @type {import('next').NextConfig} */
 
module.exports = {
  experimental: {
    serverActions: {
      bodySizeLimit: '3mb',
    },
  },
}
```

## 参考

https://nextjs-org.translate.goog/docs/app/api-reference/config/next-config-js/serverActions?_x_tr_sl=auto&_x_tr_tl=ja&_x_tr_hl=ja&_x_tr_hist=true#bodysizelimit
