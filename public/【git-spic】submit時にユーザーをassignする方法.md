---
title: 【git-spic】submit時にユーザーをassignする方法
tags:
  - git-spice
private: false
updated_at: '2026-01-18T23:56:56+09:00'
id: 3139448aa2a15b4872bf
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

以下のコマンドで、submit時に常に自分自身がassignされるように設定できます。

```bash
git config spice.submit.assignees $(whoami)
```

## 使い方

設定後は、通常通り`gs branch submit`を実行するだけで、自動的に自分がassignされます。

```bash
gs branch submit
```

## フラグとの併用

`--assign`フラグを使用した場合、設定値とフラグで指定した値が両方適用されます。

```bash
# 設定された自分に加えて、別のユーザーもassign
gs branch submit --assign another-user
```

## 複数のユーザーを指定

カンマ区切りで複数のユーザーを指定することも可能です。

```bash
git config spice.submit.assignees "user1,user2,user3"
```
