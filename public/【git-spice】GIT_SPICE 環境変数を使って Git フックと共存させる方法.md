---
title: 【git-spice】GIT_SPICE 環境変数を使って Git フックと共存させる方法
tags:
  - git-spice
private: false
updated_at: '2026-03-01T22:16:43+09:00'
id: 518a84c8ec6e755399ed
organization_url_name: null
slide: false
ignorePublish: false
---
## GIT_SPICE 環境変数とは

| 項目                   | 内容                                                    |
| ---------------------- | ------------------------------------------------------- |
| 変数名                 | `GIT_SPICE`                                             |
| セットされる値         | `1`                                                     |
| セットされるタイミング | git-spice がコマンドを呼び出すとき                      |
| 用途                   | Git フックなどで git-spice からの実行かどうかを検出する |

## 例：チェックアウト時にブランチを自動トラック

git-spice が `gs branch checkout` を実行すると `GIT_SPICE=1` がセットされます。`post-checkout` フックでこれを確認することで、**git-spice 自身の操作に干渉しない**自動トラッキングが実現できます。

### セットアップ手順

**前提条件**
- git-spice v0.23.0 以上
- Git フックが有効になっている（デフォルトは有効）
- リポジトリが `gs repo init` 済み

**1. フックスクリプトを作成する**

`.git/hooks/post-checkout` を以下の内容で作成します。
```bash
#!/usr/bin/env bash
set -euo pipefail

# post-checkout の引数:
#   $1 - 以前の HEAD の ref
#   $2 - 新しい HEAD の ref
#   $3 - ブランチのチェックアウトなら 1、ファイルなら 0
shift # old SHA
shift # new SHA
checkout_type=$1

# ファイルのチェックアウトは無視
if [[ "$checkout_type" -eq 0 ]]; then
    exit 0
fi

# git-spice の操作中は干渉しない ← GIT_SPICE 環境変数を確認
if [[ -n "${GIT_SPICE:-}" ]]; then
    exit 0
fi

# 現在のブランチ名を取得
branch_name=$(git rev-parse --abbrev-ref HEAD 2>/dev/null || echo "")
if [[ -z "$branch_name" ]]; then
    exit 0
fi

# ローカルブランチかチェック
if ! git show-ref --verify --quiet refs/heads/"$branch_name"; then
    exit 0
fi

# trunk ブランチはトラック対象外
trunk_name=$(gs trunk -n 2>/dev/null || echo "master")
if [[ "$branch_name" == "$trunk_name" ]]; then
    exit 0
fi

# 未トラックなら自動トラック
if ! git rev-parse --verify --quiet refs/spice/data:branches/"$branch_name" >/dev/null; then
    echo >&2 "Branch not tracked with git-spice: '$branch_name'. Tracking it now..."
    gs downstack track "$branch_name"
fi
```

**2. 実行権限を付与する**
```bash
chmod +x .git/hooks/post-checkout
```

**3. 動作確認**
```bash
git checkout -b my-feature main
# → 自動的に git-spice でトラックされる
```

## 参考

https://abhinav.github.io/git-spice/community/recipes/#auto-track-branches-on-checkout

https://abhinav.github.io/git-spice/changelog/#v0.23.0
