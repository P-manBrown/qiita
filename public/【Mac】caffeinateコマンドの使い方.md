---
title: 【Mac】caffeinateコマンドの使い方
tags:
  - Mac
private: false
updated_at: '2025-05-27T23:29:08+09:00'
id: 59df74a97f28f9f06e1f
organization_url_name: null
slide: false
ignorePublish: false
---

`caffeinate`コマンドを使用するとスリープしないようにできます。

https://keith.github.io/xcode-man-pages/caffeinate.8.html

## 1時間（3600秒）スリープしないようにする

```terminal
caffeinate -u -t 3600
```

## コマンドが完了するまでスリープしないようにする

```terminal
caffeinate -s "command"
```

##   指定したPIDのプロセスが完了するまでスリープしないようにする

```terminal
caffeinate -w pid
```

##   スリープしないようにする（`Ctrl + c`で終了）

```terminal
caffeinate -i
```

## ディスクがスリープしないようにする（`Ctrl + c`で終了）

```terminal
caffeinate -m
```
