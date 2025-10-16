---
title: 【Mac】shortcutsコマンドの使い方
tags:
  - Mac
private: false
updated_at: '2025-06-24T23:53:11+09:00'
id: 00f2d9292fc2262f851a
organization_url_name: null
slide: false
ignorePublish: false
---
`shotcuts`コマンドを使用するとShortcuts.appのショートカットを管理できます。

https://support.apple.com/guide/shortcuts-mac/run-shortcuts-from-the-command-line-apd455c82f02/mac

## 指定したショートカットを実行

```terminal
shortcuts run "ショートカット名"
```
## すべてのショートカットを表示

```terminal
shortcuts list
```

## すべてのフォルダを表示

```terminal
shortcuts list --folders
```

## 指定したショートカットをエディタで開く

```terminal
shortcuts view "ショートカット名"
```
