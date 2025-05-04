---
title: 【Linux】ディレクトリの一覧を取得する方法
tags:
  - Linux
  - Linuxコマンド
  - 初学者
private: false
updated_at: '2023-01-24T23:52:00+09:00'
id: 6c63ec89c95efbc0ac6a
organization_url_name: null
slide: false
ignorePublish: false
---
## `ls`コマンド

```zsh
ls -F [パス] | grep /
```
隠しファイルも含めて表示
```zsh
ls -aF [パス] | grep /
```
```zsh:サンプル
$ ls -F path/to/sample | grep /
app/
bin/
config/
db/
lib/
log/
public/
spec/
storage/
templates/
test/
tmp/
vendor/

$ ls -aF path/to/sample | grep /
./
../
.devcontainer/
.docker/
.git/
.vscode/
app/
bin/
config/
db/
lib/
log/
public/
spec/
storage/
templates/
test/
tmp/
vendor/
```

または次のように実行します。

```
$ ls -lR ./ | grep ^d
drwxr-xr-x 2 root root 44 12月  6 20:48 dir1
drwxr-xr-x 2 root root 44 12月  6 21:33 dir2
drwxr-xr-x 2 root root 6 12月  6 21:36 dir1-1
drwxr-xr-x 2 root root 6 12月  6 21:36 dir1-2
drwxr-xr-x 2 root root 6 12月  6 21:36 dir2-1
drwxr-xr-x 2 root root 6 12月  6 21:36 dir2-2

```

## `find`コマンド

`find`コマンドでディレクトリのみの一覧を取得するには次のように実行します。

```terminal
$ find ./ -mindepth 1 -type d
./app
./bin
./config
./db
./lib
./log
./public
./spec
./storage
./templates
./test
./tmp
./vendor
```
