---
title: 【Mac】dfコマンドの使い方
tags:
  - 'Mac'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

`df`コマンドを使用するとファイルシステムのディスク使用量の概要を表示できます。

 https://keith.github.io/xcode-man-pages/df.1.html

##  すべてのファイルシステムとそのディスク使用量を 512 バイト単位で表示

```terminal
df
```

##  人間が読める単位（1024 の累乗ベース）を使用して総計を表示

```terminal
df -h -c
```

## 人が読める単位（1000の累乗）を使用して総計を表示

```terminal
df --si|-H
```

## 特定のファイルまたはディレクトリを含むファイルシステムとそのディスク使用量を表示

```terminal
df path/to/file_or_directory
```
