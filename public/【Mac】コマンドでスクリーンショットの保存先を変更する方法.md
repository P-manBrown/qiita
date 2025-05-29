---
title: 【Mac】コマンドでスクリーンショットの保存先を変更する方法
tags:
  - 'Mac'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

## 保存先を変更する

以下のコマンドを実行するとスクリーンショットの保存先を変更できます。

```terminal
defaults write com.apple.screencapture location 保存先パス
```

次の場合には`~/Downloads/`に変更されます。

```terminal
defaults write com.apple.screencapture location ~/Downloads/
```

## 保存先を確認する

現在の保存先を確認するには以下のコマンドを実行します。

```terminal
defaults read com.apple.screencapture location
```

```terminal
$ defaults read com.apple.screencapture location
~/Downloads/
```
