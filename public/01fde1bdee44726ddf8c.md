---
title: 【Shell】ログインシェルの確認方法
tags:
  - Mac
  - Linux
  - shell
private: false
updated_at: '2023-05-26T22:53:06+09:00'
id: 01fde1bdee44726ddf8c
organization_url_name: null
slide: false
ignorePublish: false
---

## Linux

Linuxの場合には次のコマンドで確認できます。

```terminal
$ grep $USER /etc/passwd

```

また`SHELL`環境変数　にデフォルトでログインシェルのフルパスが設定されています。

```terminal
$ echo $SHELL
/bin/bash
```

## Mac

Macの場合には次のコマンドで確認できます。

```terminal
$ dscl localhost -read Local/Default/Users/$USER UserShell
```
