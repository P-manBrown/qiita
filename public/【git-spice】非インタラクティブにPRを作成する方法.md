---
title: 【git-spice】非インタラクティブにPRを作成する方法
tags:
  - 'git-spice'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
##  `--fill`

```bash
gs stack submit --fill
```

`--fill`フラグを使用すると、既存のコミットメッセージから自動的にPRのタイトルと本文を入力します。

### 例
```bash
# 良いコミットメッセージの例
git commit -m "Fix user login validation

- Add email format validation
- Improve error messages
- Update unit tests"

# このコミットから自動でPRが作成される
gs stack submit --fill
```

## `--title` `--body`

```bash
gs branch submit \
    --title "Add user authentication" \
    --body "This PR implements OAuth2 authentication for user login"
```

タイトルと本文を直接指定してPRを作成します。

### 例
```bash
# 通常のPR作成
gs branch submit \
    --title "Implement user profile API" \
    --body "Add REST API endpoints for user profile management

Features:
- GET /api/profile - Get user profile
- PUT /api/profile - Update user profile
- Validation and error handling included"

# ドラフトPRとして作成
gs branch submit \
    --title "WIP: Database migration" \
    --body "Work in progress for user table schema updates" \
    --draft
```
