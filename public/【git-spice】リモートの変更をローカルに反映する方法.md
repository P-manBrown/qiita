---
title: 【git-spice】リモートの変更をローカルに反映する方法
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

git-spiceは、Gitブランチをスタック管理するためのコマンドラインツールです。本記事では、リモートリポジトリの最新変更をローカルに同期する`gs repo sync`コマンドについて説明します。

## gs repo syncとは

`gs repo sync`は、リモートから最新の変更を取得（pull）するコマンドです。エイリアスとして`gs r s`も使用できます。

```bash
gs repo sync [flags]
```

## 主な機能

### 1. リモートからの変更取得

リモートブランチの最新変更をローカルに同期します。

### 2. マージ済みブランチの自動削除

同期後、マージ済みのChange Request（Pull Request）に関連するブランチは自動的に削除されます。

### 3. リスタック機能

`--restack`フラグを使用すると、同期後に現在のスタックを自動的にリスタック（再配置）できます。

```bash
gs repo sync --restack
```

## 使用上の注意

- **リモート設定が必要**: リポジトリにリモートが関連付けられている必要があります
- リモートが未設定の場合は、初期化時にプロンプトで設定を求められます

## 設定オプション

同期時のクローズされたChange Requestの処理方法は、設定で変更できます。

```bash
spice.repoSync.closedChanges
```
