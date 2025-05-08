---
title: 【Mac】特定のファイルやフォルダを非表示にする方法
tags:
  - Mac
private: false
updated_at: '2025-05-08T23:48:35+09:00'
id: 95ba9c2cfaaf5d5ba93d
organization_url_name: null
slide: false
ignorePublish: false
---

## ファイルやフォルダを非表示にする

以下のコマンドを実行するとファイルやフォルダを非表示にできます。

```terminal
chflags hidden ファイルやフォルダのパス
```

## 再度表示する

非表示にしたファイルやフォルダを再度表示するには以下のコマンドを実行します。

```terminal
chflags nohidden ファイルやフォルダのパス
```
