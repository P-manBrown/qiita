---
title: 【git-spice】submit時に自動でreviewerを設定する方法
tags:
  - git-spice
private: false
updated_at: '2026-01-19T23:03:29+09:00'
id: 369871260f45b399f9ce
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

### フラグで指定する方法

`gs branch submit`コマンドに`--reviewer`フラグを追加することで、reviewerを指定できます。

```bash
# 個人のreviewerを指定
gs branch submit --reviewer username

# チームのreviewerを指定（GitHub）
gs branch submit --reviewer org/team-name
```

### 設定ファイルで指定する方法

毎回フラグを指定するのが面倒な場合は、`git config`で設定しておくと便利です。

```bash
# 個人のreviewerを設定
git config spice.submit.reviewers 'username'

# チームのreviewerを設定
git config spice.submit.reviewers 'example/my-team'
```

## 例

### チーム全体に常にレビュー依頼を送る

```bash
git config spice.submit.reviewers 'myorg/backend-team'
```

この設定をしておくと、`gs branch submit`を実行するたびに、自動的にbackend-teamにレビュー依頼が送られます。

### 複数のreviewerを設定する

カンマ区切りで複数のreviewerを指定できます。

```bash
git config spice.submit.reviewers 'alice,bob,myorg/frontend-team'
```

### フラグと設定ファイルの組み合わせ

設定ファイルで基本的なreviewerを設定しつつ、フラグで追加のreviewerを指定することもできます。両方の値がマージされます。

```bash
# 設定ファイルでチームを設定
git config spice.submit.reviewers 'myorg/my-team'

# 実行時に個別のreviewerを追加
gs branch submit --reviewer alice
# → myorg/my-teamとaliceの両方がreviewerに設定される
```

## 参考

https://abhinav.github.io/git-spice/cli/config/#spicesubmitreviewers
