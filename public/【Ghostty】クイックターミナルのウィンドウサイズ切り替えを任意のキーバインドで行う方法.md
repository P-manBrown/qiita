---
title: 【Ghostty】クイックターミナルのウィンドウサイズ切り替えを任意のキーバインドで行う方法
tags:
  - ghostty
private: false
updated_at: '2026-01-24T23:56:05+09:00'
id: 72ca4db402e450bf3e2c
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

設定ファイルに以下のように追記すると`shift+escape`でウィンドウサイズを切り替えられます。

```
keybind = shift+escape=toggle_fullscreen
```

![screen-recording-133.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/b1c529c4-3553-485f-9ca5-fb69d6012ec3.gif)

## 参考

https://ghostty.org/docs/config/keybind/reference#toggle_fullscreen
