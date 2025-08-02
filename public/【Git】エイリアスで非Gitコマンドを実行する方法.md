---
title: 【Git】エイリアスで非Gitコマンドを実行する方法
tags:
  - Git
private: false
updated_at: '2025-08-02T23:27:25+09:00'
id: 97302706b716197bcae4
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

Gitエイリアスで非Gitコマンドを実行するには、コマンドの先頭に`!`（エクスクラメーションマーク）を付けます。

### コマンドラインから設定

```bash
git config --global alias.エイリアス名 '!コマンド'
```

```bash
# 例：ls コマンドを実行
git config --global alias.ls '!ls -la'

# 実行
git ls
```

### 設定ファイルに直接記述

`~/.gitconfig`ファイルを編集して設定することも可能です。

```ini
[alias]
    ls = !ls -la
```

```bash
# 実行
git ls
```

## 参考

https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases
