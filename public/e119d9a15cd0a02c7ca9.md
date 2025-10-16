---
title: 【git-spice】ブランチの表示順を設定する方法
tags:
  - git-spice
private: false
updated_at: '2025-09-03T22:38:05+09:00'
id: e119d9a15cd0a02c7ca9
organization_url_name: null
slide: false
ignorePublish: false
---
`gs branch onto`や`gs branch checkout`などのコマンドでブランチ名を指定しない場合、プロンプトが表示されます。この時のブランチ表示順序を設定できます。

## 設定方法

```bash
# リポジトリレベル
git config --local spice.branchPrompt.sort <ソート方法>

# グローバルレベル
git config --global spice.branchPrompt.sort <ソート方法>
```
以下のような値が使用できます。

- committerdate: コミット日付で並べ替え
- refname:ブランチ名で並べ替え（初期設定値）
- authordate: 最初にコミットした日付で並べ替え


先頭に`-`を付けると降順になります。

```bash
# 最新のコミットが上位
git config spice.branchPrompt.sort -committerdate

# ブランチ名の逆順
git config spice.branchPrompt.sort -refname
```

## 設定確認

```bash
git config spice.branchPrompt.sort
```
