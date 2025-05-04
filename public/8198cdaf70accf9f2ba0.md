---
title: 【Linux】ファイルの特定の行のみ取得する方法
tags:
  - Linux
  - 初学者
private: false
updated_at: '2022-10-13T20:06:16+09:00'
id: 8198cdaf70accf9f2ba0
organization_url_name: null
slide: false
ignorePublish: false
---
## 1行目のみ取得する

ファイルの1行目のみ取得するには以下のように実行します。

```zsh
head -n 1 対象ファイルパス
```

## 指定した行のみ取得する

指定した行のみ取得するには以下のようにします。

```zsh
sed -n 行数p 対象ファイルパス
```

`./sample.txt`の5行目を取得する場合には以下のように実行します。

```zsh
sed -n 5p ./sample.txt
```

## 指定した行以降を取得する

指定した行以降を取得するには以下のようにします。

```zsh
sed -n '開始行,$p' 対象ファイル
```

`./sample.txt`の5行目以降を取得するためには以下のように実行します。

```zsh
sed -n '5,$p' ./sample.txt
```
