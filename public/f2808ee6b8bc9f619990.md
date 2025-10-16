---
title: 【Mac】スクリーンショットのファイル形式を変更する方法
tags:
  - Mac
private: false
updated_at: '2025-05-14T23:53:32+09:00'
id: f2808ee6b8bc9f619990
organization_url_name: null
slide: false
ignorePublish: false
---

## JPEGに変更

以下のコマンドを実行するとスクリーンショットのファイル形式を`JPEG`に変更できます。

```terminal
defaults write com.apple.screencapture "type" -string "jpg"
```

## PNGに変更

以下のコマンドを実行すると`PNG`に変更できます。

```terminal
defaults write com.apple.screencapture "type" -string "png"
```
