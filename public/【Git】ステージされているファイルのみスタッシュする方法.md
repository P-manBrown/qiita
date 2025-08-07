---
title: 【Git】ステージされているファイルのみスタッシュする方法
tags:
  - 'Git'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 方法

`git stash --staged` コマンドを使用することで、ステージングエリアに追加されているファイルのみをスタッシュできます。これにより、作業ディレクトリの未ステージの変更を残したまま、ステージされた変更だけを一時退避できます。

```bash
git stash --staged
```

## 例

実行前

```bash
# ファイルの状態を確認
$ git status

# 出力例:
# On branch main
# Changes to be committed:
#   (use "git restore --staged <file>..." to unstage)
#         modified:   src/main.js
#         new file:   src/utils.js
#
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#         modified:   README.md
#         modified:   package.json
```

ステージされたファイルのみをスタッシュ

```bash
# ステージされた変更をスタッシュ
$ git stash --staged

# または、メッセージ付きでスタッシュ
$ git stash --staged -m "機能追加のステージされた変更を一時保存"
```

| オプション     | 説明                                   |
| -------------- | -------------------------------------- |
| `--staged`     | ステージされたファイルのみをスタッシュ |
| `-m <message>` | スタッシュにメッセージを追加           |

実行後

```bash
$ git status

# 出力例:
# On branch main
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#         modified:   README.md
#         modified:   package.json
#
# nothing added to commit but untracked files present (use "git add" to track)
```

## 参考

https://git-scm.com/docs/git-stash#Documentation/git-stash.txt---staged
