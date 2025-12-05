---
title: 【Zed】ウィンドウの背景を透過する方法
tags:
  - ZedEditor
private: false
updated_at: '2025-12-05T22:48:36+09:00'
id: 54aed1044011364bf0a9
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`background.appearance`という設定を使用してウィンドウの背景を透過させることができます。

**透過**

```json
{
  "experimental.theme_overrides": {
    "background.appearance": "transparent"
  }
}
```

**ぼかし**

```json
{
  "experimental.theme_overrides": {
    "background.appearance": "blurred"
  }
}
```

完全な透過効果を得るには、`background`や`editor.background`なども透過色に設定する必要があります。

```json
{
  "experimental.theme_overrides": {
    "background.appearance": "blurred",
   	"background": "#00000000",
    "editor.background": "#00000000"
  }
}
```

上記の場合にはエディター部分のみ透過されます。

## 参考

https://github.com/zed-industries/zed/issues/38995
