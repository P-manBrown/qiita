---
title: 【Mac】statコマンドの使い方
tags:
  - Mac
private: false
updated_at: '2025-06-10T22:03:48+09:00'
id: 5ce8580c62fd26ef911e
organization_url_name: null
slide: false
ignorePublish: false
---

`stat`コマンドを使用するとファイルのステータスが表示されます。

https://keith.github.io/xcode-man-pages/stat.1.html

## ファイルのサイズ、パーミッション、作成日時、アクセス日時など、各種プロパティを表示

```terminal
stat path/to/file
```

## より詳細に表示（Linux の stat に近い形式）

```terminal
stat -x path/to/file
```

## ファイルパーミッションを 8 進数のみで表示

```terminal
stat -f %Mp%Lp path/to/file
```

## ファイルの所有者とグループを表示

```terminal
stat -f "%Su %Sg" path/to/file
```

## ファイルのサイズをバイト単位で表示

```terminal
stat -f "%z %N" path/to/file
```
