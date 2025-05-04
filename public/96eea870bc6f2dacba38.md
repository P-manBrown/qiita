---
title: 【Next.js】クライアントコンポーネントにインポートされた際にエラーを発生させる方法
tags:
  - Next.js
private: false
updated_at: '2023-12-12T23:58:44+09:00'
id: 96eea870bc6f2dacba38
organization_url_name: null
slide: false
ignorePublish: false
---
`server-only`をimportすることでコンポーネントがクライアントコンポーネントにインポートされた際にエラーが発生するようになります。

`server-only`をインストールします。

```terminal
npm i server-only
```

`server-only`をインポートします。

```
import "server-only"
```

また、以下のように`import "client-only"`を記述することでコンポーネントがサーバーサイドで実行された際にエラーが発生するようにできます。

```
import "client-only"
```
