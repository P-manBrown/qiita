---
title: 【Mac】スクリーンショットのドロップシャドウを無効にする方法
tags:
  - 'Mac'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

## 無効にする方法

以下のコマンドを実行するとウィンドウのスクリーンショットを撮影した際のドロップシャドウが削除されます。

```terminal
defaults write com.apple.screencapture disable-shadow -bool true && killall SystemUIServer
```

## 実行前

![CDA3809A-7307-4BDE-9B78-542189D3B2C0.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/20ecb311-2eba-46d0-a1af-042814a38d45.png)

## 実行後

![F301D01A-D0B2-4071-9FF5-FCCF542DBB8F.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/722df99e-f62f-4edb-b88f-5be2cc454590.png)

## 元に戻す方法

ドロップシャドウを元に戻すには以下のコマンドを実行します。

```terminal
defaults write com.apple.screencapture disable-shadow -bool false && killall SystemUIServer
```
