---
title: 【Mac】CLIでデスクトップのウィジェットを非表示にする方法
tags:
  - 'Mac'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 非表示にする

以下のコマンドを実行するとデスクトップウィジェットが非表示になります。

```shell
defaults write com.apple.WindowManager StandardHideWidgets -bool true
```

## 表示する

表示する場合は以下のコマンドを実行します。

```shell
defaults write com.apple.WindowManager StandardHideWidgets -bool false
```

## 現在の設定値を確認する

現在の設定値を確認するには以下のコマンドを実行します。

```shell
defaults read com.apple.WindowManager StandardHideWidgets
```
