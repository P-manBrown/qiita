---
title: 【Git】ステージされていないファイルのみをスタッシュする方法
tags:
  - 'Git'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## コマンド

`git stash --keep-index --include-untracked` でステージされていない変更のみをスタッシュできます。ステージエリアの内容を保持したまま、未ステージの変更や追跡されていないファイルを一時的に退避できます。


### `--keep-index` オプション

- ステージされた変更はスタッシュされずに作業ディレクトリに残る

### `--include-untracked` オプション

- 追跡されていないファイル（新規作成ファイル）もスタッシュに含める
- 通常の `git stash` では追跡されていないファイルは対象外となる

## 例

実行前

```bash
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
    modified:   src/main.js
    new file:   src/utils.js

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
    modified:   README.md
    modified:   package.json

Untracked files:
  (use "git add <file>..." to include in what will be committed)
    temp.txt
    debug.log
```

コマンド実行

```bash
$ git stash --keep-index --include-untracked
Saved working directory and index state WIP on main: abc1234 Previous commit message
```

実行後

```bash
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
    modified:   src/main.js
    new file:   src/utils.js

# 未ステージの変更と追跡されていないファイルが消えている
```

## 参考

https://git-scm.com/docs/git-stash#Documentation/git-stash.txt---keep-index

https://git-scm.com/docs/git-stash#Documentation/git-stash.txt---include-untracked
