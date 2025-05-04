---
title: 【Linux】検索したファイルに対してコマンドを実行する方法
tags:
  - Linux
  - Linuxコマンド
  - 初学者
private: false
updated_at: '2023-01-21T23:51:31+09:00'
id: d21a0ba6b29e0af6fbd0
organization_url_name: null
slide: false
ignorePublish: false
---
## `exec`オプション
`find`コマンドの`exec`オプションを使用することで取得したパスに対してコマンドを実行できます。

以下のように記述すると取得したパス一つ一つに対してコマンドが実行されます。

```zsh
find . -name "*.txt" -exec rm {} \;
```
実際に実行されるコマンドは以下のようになります。

```zsh
$ rm "./sample1.txt"
$ rm "./sample2.txt"
$ rm "./sample3.txt" 
$ rm "./sample4.txt"
$ rm "./sample5.txt"
```

以下のようにすると取得したパスを並べた状態で引数として実行します。

```zsh
find . -name "*.txt" -exec rm {} +
```
実際に実行されるコマンドは以下のようになります。
```zsh
$ rm "./sample1.txt" "./sample2.txt" "./sample3.txt" "./sample4.txt" "./sample5.txt"
```

## `xargs`コマンド
また`xargs`コマンドを使用することで取得したパスに対してコマンドを実行できます。

```
find . -name "*.txt" | xargs rm
```

上記のように記述すると以下のように`rm`が実行されます。

```zsh
$ rm "./sample1.txt" "./sample2.txt" "./sample3.txt" "./sample4.txt" "./sample5.txt"
```

取得したファイルパス一つ一つに対して実行したい場合には以下のようにします。

```
find . -name "*.txt" | xargs -L 1 rm
```
```zsh
$ rm "./sample1.txt"
$ rm "./sample2.txt"
$ rm "./sample3.txt" 
$ rm "./sample4.txt"
$ rm "./sample5.txt"
```
