---
title: 【Mac】openコマンドの使い方
tags:
  - 'Mac'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

`open`コマンドを使用するとファイル、ディレクトリ、アプリケーションを開くことができます。

##   デフォルトのアプリケーションでファイルを開く

```terminal
open file.txt
```

### カレントディレクトリの特定の拡張子のファイルを全てデフォルトのアプリケーションで開く

```terminal
open *.txt
```

## 特定のアプリケーションを開く

```terminal
open -a "Safari"
```

## 特定のアプリケーションでファイルを開く

```terminal
open -a "Safari" image.gif
```

## バンドル識別子に基づいてアプリケーションを開く

```terminal
open -b com.domain.application
```

### アプリケーションの新しいインスタンスを開く

```terminal
open -n -b com.domain.application
```

## Finderでディレクトリを開く

```terminal
open path/to/dir
```

## Finderでファイルを開く

```terminal
open -R path/to/file
```
