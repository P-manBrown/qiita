---
title: 【git-spice】プルリクエストをデフォルトでドラフトとして作成するように設定する方法
tags:
  - 'git-spice'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`spice.submit.draft`という設定オプションでプルリクエストを作成する際のデフォルト動作を制御できます。

- `true`: デフォルトでドラフトとしてプルリクエストを作成
- `false`（デフォルト）: デフォルトでレビュー可能な状態でプルリクエストを作成

### グローバル設定（すべてのリポジトリに適用）

```bash
git config --global spice.submit.draft true
```

### ローカル設定（現在のリポジトリのみに適用）

```bash
git config --local spice.submit.draft true
```

### 設定確認

```bash
git config spice.submit.draft
```

## 動作の違い

### 設定前

```bash
gs submit          # レビュー可能な状態で作成
gs submit --draft  # ドラフトとして作成（明示的指定）
```

### 設定後

```bash
gs submit             # ドラフトとして作成（自動）
gs submit --no-draft  # レビュー可能な状態で作成（明示的指定）
```
