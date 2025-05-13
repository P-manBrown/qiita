---
title: 【CLI】awkコマンドの使い方
tags:
  - 'CLI'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

## スペースで区切られたファイルの 5 列目  を表示

```terminal
awk '{print $5}' path/to/file
```

## スペースで区切られたファイルの 「foo」 を含む行の 2 列目を表示

```terminal
awk '/foo/ {print $2}' path/to/file
```


## ファイル内の各行の最後の列を表示

```terminal
awk -F ',' '{print $NF}' path/to/file
```

## ファイルの最初の列の値を合計し、合計を表示

```terminal
awk '{s+=$1}. END {print s}' path/to/file
```

## 最初の行から 3 行目までを表示

```terminal
awk 'NR%3==1' path/to/file
```
