---
title: 【git-spice】コミットを作成する方法
tags:
  - 'git-spice'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

git-spiceは、Gitブランチをスタック形式で管理できるツールです。この記事では、`gs commit create`コマンドを使った新規コミットの作成方法に焦点を当てて解説します。

## gs commit createとは

`gs commit create`は、ステージされた変更を現在のブランチにコミットし、必要に応じて上位ブランチを自動的にリベースするコマンドです。

```bash
gs commit create
```

通常の`git commit`との違いは、コミット後に自動的に`gs upstack restack`が実行される点です。これにより、ブランチスタック全体の整合性が保たれます。

## 基本的な使い方

### 1. 最もシンプルな形

```bash
# 変更をステージ
git add .

# コミット作成（エディタでメッセージを入力）
gs commit create
```

### 2. コミットメッセージを直接指定

```bash
git add src/feature.js
gs commit create -m "新機能を追加"
```

### 3. 全ての変更を自動ステージしてコミット

```bash
gs commit create -a -m "すべての変更をコミット"
```

## 主要なオプション

### -m, --message

コミットメッセージを指定します。

```bash
gs commit create -m "ユーザー認証機能を実装"
```

### -a, --all

変更されたファイルを自動的にステージしてからコミットします。

```bash
gs commit create -a -m "バグ修正"
```

### --allow-empty

変更がなくても空のコミットを作成します。

```bash
gs commit create --allow-empty -m "空のコミット"
```

### --no-verify

pre-commitフックやcommit-msgフックをスキップします。

```bash
gs commit create --no-verify -m "フックをバイパス"
```
