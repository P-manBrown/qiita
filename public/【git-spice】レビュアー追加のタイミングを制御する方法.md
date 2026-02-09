---
title: 【git-spice】レビュアー追加のタイミングを制御する方法
tags:
  - git-spice
private: false
updated_at: '2026-02-09T20:08:45+09:00'
id: 591916e0ddbdb6489cc6
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`spice.submit.reviewers.addWhen`でPRにレビュアーを自動追加するタイミングが制御できます。

## 設定値

| 値 | 動作 |
|---|---|
| `always` (デフォルト) | すべてのPRにレビュアーを追加 |
| `ready` | ドラフトPRにはレビュアーを追加しない |

## 使用例

```bash
# ドラフトPRにはレビュアーを追加しない設定
git config spice.submit.reviewers.addWhen ready
```

## `ready`設定時の挙動

- 通常のPR: `spice.submit.reviewers`で設定されたレビュアーが自動追加される
- ドラフトPR: 設定されたレビュアーはスキップされる
- `--reviewer`フラグで明示的に指定した場合: ドラフトPRでも追加される

## 関連設定

`spice.submit.reviewers`: 自動追加するレビュアーのリスト(カンマ区切り)

```bash
# GitHubの場合
git config spice.submit.reviewers "username1,username2,org/team"
```

## 参考

https://abhinav.github.io/git-spice/cli/config/#spicesubmitreviewersaddwhen
