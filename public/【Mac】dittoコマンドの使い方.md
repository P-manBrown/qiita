---
title: 【Mac】dittoコマンドの使い方
tags:
  - Mac
private: false
updated_at: '2025-05-25T23:55:49+09:00'
id: b5695937da43b007e089
organization_url_name: null
slide: false
ignorePublish: false
---

`ditto`コマンドを使用するとファイルやディレクトリをコピーできます。

 https://keith.github.io/xcode-man-pages/ditto.1.html

## コピー先ディレクトリの内容をコピー元ディレクトリの内容で上書き

```terminal
ditto path/to/source_directory path/to/destination_directory
```

## コピーされる各ファイルごとにターミナルウィンドウに1行出力

```terminal
ditto -V path/to/source_directory path/to/destination_directory
```

## 元のファイルパーミッションを保持したままファイルまたはディレクトリをコピー

```terminal
ditto -rsrc path/to/source_directory path/to/destination_directory
```
