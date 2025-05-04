---
title: ファビコンを取得する方法
tags:
  - favicon
private: false
updated_at: '2023-06-16T01:36:33+09:00'
id: aae61f87fbffd8753f5a
organization_url_name: null
slide: false
ignorePublish: false
---
## 取得方法

以下のURLにファビコンを取得したいサイトのドメインまたはURLを末尾に追記するとファビコンが別のタブで表示されます。

```
http://www.google.com/s2/favicons?domain=ファビコンを取得したいサイトのURL
```
ファビコンのサイズは16x16ですが、表示されたタブのURL末尾の`size=`の値を変更することで別のサイズを取得できます。

```
https://t2.gstatic.com/faviconV2?client=SOCIAL&type=FAVICON&fallback_opts=TYPE,SIZE,URL&url=ファビコンを取得したいサイトのURL&size=64

```

上記の場合には64x64が表示されます。
