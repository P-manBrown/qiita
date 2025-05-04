---
title: 【Git】リポジトリ専用のGit Aliasesを設定する方法
tags:
  - Git
private: false
updated_at: '2024-11-14T23:54:50+09:00'
id: ff8fcbd5d9d42f070ff6
organization_url_name: null
slide: false
ignorePublish: false
---
## リポジトリ専用のGit Aliasesを設定する方法

```terminal
git config --local alias.ci commit
```

設定したリポジトリでのみ `git ci` で　`git commit` が実行できる。

## 外部コマンドにエイリアスを設定する

外部コマンドにエイリアスを設定する場合にはコマンドの最初に `!` を記述する必要がある。

```terminal
git config --local alias.sync "!git switch main && git pull --prune && git branch --format '%(refname:short) %(upstream:track)' | grep -oP '.*(?=\s\[gone\]$)' | xargs -r git branch -D"
```

設定したリポジトリで `git sync` で `git switch main && git pull --prune && git branch --format '%(refname:short) %(upstream:track)' | grep -oP '.*(?=\s\[gone\]$)' | xargs -r git branch -D` が実行できる。

## 参考

https://git-scm.com/book/ja/v2/Git-%E3%81%AE%E5%9F%BA%E6%9C%AC-Git-%E3%82%A8%E3%82%A4%E3%83%AA%E3%82%A2%E3%82%B9
