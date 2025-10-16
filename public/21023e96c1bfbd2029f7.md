---
title: 【git-spice】ブランチ名を変更する方法
tags:
  - git-spice
private: false
updated_at: '2025-08-09T22:13:15+09:00'
id: 21023e96c1bfbd2029f7
organization_url_name: null
slide: false
ignorePublish: false
---
## 変更方法

git-spiceでブランチ名を変更するには、`gs branch rename`コマンドを使用します。

### 指定したブランチの名前を変更

既存のブランチ名を新しい名前に変更するには以下のようにします。

```bash
gs branch rename <old-name> <new-name>
```

例：
```bash
gs branch rename feature-old feature-new
```

### 現在のブランチ名を変更

現在チェックアウトしているブランチの名前を変更には以下のようにします。

```bash
gs branch rename <new-name>
```

例：
```bash
gs branch rename feature-improved
```

### インタラクティブに変更

プロンプトを使って対話的にブランチ名を変更には以下のようにします。

```bash
gs branch rename
```

git-spiceが現在のブランチ名の変更をインタラクティブに案内してくれます。

## コマンドエイリアス

`gs branch rename`は以下の短縮形でも実行できます。

- `gs branch rn`
- `gs branch mv`

```bash
# これらは全て同じ動作をします
gs branch rename feature-old feature-new
gs branch rn feature-old feature-new
gs branch mv feature-old feature-new
```

## git branch -m を使った場合の対処

通常のGitコマンド（`git branch -m`）でブランチ名を変更した場合、git-spiceはその変更を自動的に認識しません。この場合は、以下のコマンドを使用してブランチのトラッキング状態を手動で更新する必要があります。

```bash
# 古いブランチ名のトラッキングを解除
gs branch untrack <old-branch-name>

# 新しいブランチ名でトラッキングを開始
gs branch track <new-branch-name>
```

## 参考

https://abhinav.github.io/git-spice/cli/reference/#gs-branch-rename
