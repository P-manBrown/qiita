---
title: 【Mac】duコマンドの使い方
tags:
  - Mac
private: false
updated_at: '2025-05-30T23:47:59+09:00'
id: e2b718b2d6264fa2cdb0
organization_url_name: null
slide: false
ignorePublish: false
---

`du`コマンドを使用するとファイルやディレクトリのサイズを確認できます。

## ディレクトリとサブディレクトリのサイズを指定した単位 (KiB/MiB/GiB) で一覧表示

```terminal
du -k|m|g path/to/directory
```

## ディレクトリとサブディレクトリのサイズを人間が読める形式で一覧表示

```terminal
du -h path/to/directory
```

## 単一のディレクトリのサイズを人間が読める単位で表示

```terminal
du -sh path/to/directory
```

## 特定のディレクトリとその中にあるすべてのファイルとディレクトリのサイズを人間が読める単位で表示

```terminal
du -ah path/to/directory
```

## ディレクトリとその中にあるすべてのファイルとディレクトリの人間が読めるサイズを指定したレベルまで表示

```terminal
du -h -d 2 path/to/directory
```

## 現在のディレクトリのサブディレクトリにあるすべての .jpg ファイルの人間が読めるサイズを一覧表示し累計を表示

```terminal
du -ch */*.jpg
```
