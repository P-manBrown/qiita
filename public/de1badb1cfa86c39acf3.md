---
title: 【Fish】PATHを管理する方法
tags:
  - fish
private: false
updated_at: '2025-04-24T23:59:37+09:00'
id: de1badb1cfa86c39acf3
organization_url_name: null
slide: false
ignorePublish: false
---
## 追加

`fish_add_path`コマンドを使用することで、`$PATH`に新しいディレクトリを追加できます。

```fish
fish_add_path path ...
```

### オプション

- `-a` または `--append`: コンポーネントを変数の末尾に追加します
- `-p` または `--prepend`: コンポーネントを変数の先頭に追加します（デフォルト）
- `-g` または `--global`: グローバルな `fish_user_paths` を使用します
- `-U` または `--universal`: ユニバーサルな `fish_user_paths` を使用します（デフォルト）
- `-P` または `--path`: `$PATH` を直接操作します
- `-m` または `--move`: 既存のコンポーネントを追加されるべき位置に移動します
- `-v` または `--verbose`: 使用された `set` コマンドを表示します
- `-n` または `--dry-run`: 実行せずに使用される `set` コマンドを表示します
- `-h` または `--help`: このコマンドの使い方に関するヘルプを表示します

### 新しいディレクトリを`$PATH`に追加する

新しいアプリケーションをインストールした後、そのバイナリを`$PATH`に追加するには、次のようにします。

```terminal
fish_add_path /opt/mycoolthing/bin
```

### ユーザーのローカルバイナリを優先する

`~/.local/bin`を最初にチェックさせたい場合は、次のようにします。

```terminal
fish_add_path -m ~/.local/bin
```

### グローバルな`fish_user_paths`を使用する

複数のディレクトリをグローバルに追加するには、次のようにします。

```terminal
fish_add_path -g ~/.local/bin ~/.otherbin /usr/local/sbin
```

### `$PATH`の末尾に追加する

フォールバック用のディレクトリを`$PATH`の末尾に追加するには、次のようにします。

```terminal
fish_add_path -aP /opt/fallback/bin
```

### 現在の作業ディレクトリの`bin`を追加する

現在の作業ディレクトリの`bin/`を追加するには、次のようにします。

```terminal
fish_add_path -v bin/
```

### HomebrewでインストールしたRubyのパスを追加する

HomebrewでインストールしたRubyのバイナリを`$PATH`に追加するには、次のようにします。

```terminal
fish_add_path /usr/local/opt/ruby/bin
```

## 削除

### パスを確認する
以下のようにパスの一覧を確認できます。

```terminal
$ echo $fish_user_paths | tr " " "\n" | nl
     1  /usr/local
     2  /usr/sbin
     3  /usr/local/bin
     4  /home/username/.nodebrew/current/bin
     5  /home/username/.pyenv/shims
     6  /home/username/.pyenv/bin
     7  /home/username/.yarn/bin
```

### パスを削除する
`set -e`, `set --erase`を使用してパスを削除できます。
インデックスを指定して特定のパスを削除します。
インデックスは`0`からではなく`1`からです。

```terminal
set -e fish_user_paths[1]
```

複数のパスを削除する場合には指定するべきインデックスが変更されるため、`echo $fish_user_paths | tr " " "\n" | nl`で確認する必要があります。
