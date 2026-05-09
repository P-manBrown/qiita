---
title: 【git-spice】フォークワークフロー
tags:
  - git-spice
private: false
updated_at: '2026-05-09T23:08:47+09:00'
id: 22e559023e69e796503f
organization_url_name: null
slide: false
ignorePublish: false
---

## セットアップ方法

### リモートの役割を理解する

フォークワークフローでは、2種類のリモートを使い分けます。

| リモート | 指す先 | 役割 |
|---|---|---|
| `upstream` | 本家リポジトリ | PRの受け先、trunkの取得元 |
| `origin` | 自分のフォーク | ブランチのプッシュ先 |

### リポジトリの初期化

`gs repo init` に `--upstream` と `--remote` オプションを渡すことで、それぞれの役割を明示的に設定します。

```bash
$ gs repo init --upstream upstream --remote origin
```

- `--upstream upstream` : PRを受け取るリモートを `upstream` に指定
- `--remote origin` : ブランチをプッシュするリモートを `origin` に指定

これだけで設定は完了です。

### 注意：GitHub App認証との非互換性

GitHubのフォークワークフローでは、**GitHub App認証はサポートされていません**。Personal Access Token（PAT）やOAuthなど、他の認証方法を使用してください。

## 通常のPR提出との違い

初期化後は、これまでと同じコマンドでブランチを提出できます。内部動作が変わるだけです。

```bash
# 現在のブランチをPR提出する
$ gs branch submit --fill
INF Created #123: https://github.com/example/project/pull/123
```

git-spiceが自動的に：

- ブランチを `origin`（フォーク）にプッシュ
- `upstream`（本家）に対してPRを作成

してくれます。`--fill` フラグはコミットメッセージからタイトルと本文を自動入力するオプションです。

## スタック提出時の挙動

フォークワークフローでスタック全体を提出するときは、少し挙動が異なります。

```bash
$ git branch --show-current
feature-a

$ gs stack submit --fill
INF Created #123: https://github.com/example/project/pull/123
INF feature-b: Pushing to origin, skipping CR: base is feature-a
```

`feature-b` はプッシュはされますが、PRは作成されません。

これはなぜかというと、フォークワークフローでは **trunkを直接ベースとするブランチのみPRが作成される** からです。`feature-b` は `feature-a` をベースにしているため、`feature-a` のPRがマージされてtrunkにリベースされるまで、PRの作成はスキップされます。

### スタック全体をPRにしたい場合

スタック全体でPRを出したい場合は、write権限を持つリポジトリを使う通常フロー、またはフォーク先のリポジトリにメンバーとして参加している場合に限り可能です。フォークワークフローではこの制限があることを念頭に置いておきましょう。

## upstreamとの同期

本家リポジトリのmainブランチを取得して最新の状態に保つには、通常どおり `gs repo sync` を使います。

```bash
$ gs repo sync
INF main: pulled 3 new commit(s)
INF feat1: #123 was merged
INF feat1: deleted (was 9f1c9af)
```

フォーク設定を行っていれば、`upstream` からtrunkを取得し、マージ済みのローカルブランチを自動で削除してくれます。

## まとめ

| 操作 | コマンド |
|---|---|
| フォークワークフローの初期化 | `gs repo init --upstream upstream --remote origin` |
| 現在のブランチをPR提出 | `gs branch submit --fill` |
| スタック全体をPR提出 | `gs stack submit --fill` |
| upstreamと同期 | `gs repo sync` |

## 参考

https://abhinav.github.io/git-spice/guide/cr/#fork-workflows
