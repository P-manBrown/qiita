---
title: 【Shell】標準出力と標準エラー出力を次のコマンドに渡す方法
tags:
  - shell
private: false
updated_at: '2025-02-19T23:59:15+09:00'
id: fea7d2b6adbe07ad60b3
organization_url_name: null
slide: false
ignorePublish: false
---
以下のように記述すると標準出力と標準エラー出力を次のコマンドに渡せます。

```sh
some_command 2>&1 | next_command
```

zshの場合以下のようにも記述できます。

```shell
some_command |& next_command
```

fishの場合以下のようにも記述できます。

```shell
some_command &| next_command
```
