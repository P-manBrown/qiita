---
title: 【Shell】行数を指定して内容を取得する方法
tags:
  - shell
  - 初学者
private: false
updated_at: '2023-04-06T23:52:15+09:00'
id: def751edafb4b75d310a
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
