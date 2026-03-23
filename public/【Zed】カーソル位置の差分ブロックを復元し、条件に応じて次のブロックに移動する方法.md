---
title: 【Zed】カーソル位置の差分ブロックを復元し、条件に応じて次のブロックに移動する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-03-23T23:13:43+09:00'
id: d15d0ffc6ca42d40ff50
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Zed エディタには、Git の差分（diff）を確認・操作するための機能が充実しています。本記事では、2026年3月にマージされた PR #50324 で導入された **`git: RestoreAndNext`** アクションについて解説します。

このアクションを使うと、カーソル位置にある差分ブロック（hunk）を元の状態に戻しながら、条件に応じて次の差分ブロックへ自動的に移動できます。`git: StageAndNext` や `git: UnstageAndNext` と同様のコンセプトを「復元（restore）」にも適用したものです。

## `git: RestoreAndNext` とは

### 概要

`git: RestoreAndNext` は、以下の2つの操作をひとつのアクションにまとめたものです。

1. カーソルが置かれている差分ブロック（hunk）を復元（restore）する
2. 復元後、次の差分ブロックへカーソルを移動する（条件によってラップアラウンドする）

これにより、ファイル内に複数の差分ブロックがある場合に、ひとつずつ確認しながら不要な変更を素早く取り消せます。

### 類似アクションとの比較

| アクション | 操作内容 |
|---|---|
| `git: Stage` | カーソル位置の hunk をステージングする |
| `git: StageAndNext` | ステージング後、次の hunk へ移動する |
| `git: Unstage` | カーソル位置の hunk をアンステージングする |
| `git: UnstageAndNext` | アンステージング後、次の hunk へ移動する |
| `git: Restore` | カーソル位置の hunk を復元する |
| **`git: RestoreAndNext`** | **復元後、次の hunk へ移動する（新機能）** |

## デフォルトキーバインド

このアクションの導入に伴い、**Git Diff ビュー限定**でデフォルトのキーバインドが変更されました。

| プラットフォーム | キーバインド | アクション |
|---|---|---|
| macOS | `cmd-alt-z` | `git: RestoreAndNext`（Git Diff ビュー内） |
| Linux / Windows | `ctrl-k ctrl-r` | `git: RestoreAndNext`（Git Diff ビュー内） |

注意点として、このキーバインドが `git: RestoreAndNext` に変更されるのは **Git Diff ビューにフォーカスがある場合のみ**です。通常のファイル編集画面やマルチバッファでは、従来の `git: Restore` の動作が維持されます。

## ラップアラウンドの挙動

`RestoreAndNext` は次の hunk に移動する際、**ラップアラウンド**（バッファの末尾まで到達したら先頭に戻る）の動作を `StageAndNext` / `UnstageAndNext` と同じロジックで行います。

具体的には、`MultiBuffer::all_diff_hunks_expanded` が `false` を返す場合（すべての差分が展開されていない状態）はラップアラウンドせず、`true` の場合はラップアラウンドします。

```
差分ブロックが残っている場合：
  hunk A → hunk B → hunk C → hunk A（ラップアラウンド）

差分ブロックが最後の 1 つになった場合（全展開状態）：
  hunk A → 移動しない
```

## keymap.json でのカスタマイズ

デフォルトのキーバインドを変更したい場合は、`keymap.json` を編集します。

Zed のキーマップ設定は `cmd-shift-p`（macOS）または `ctrl-shift-p`（Linux/Windows）でコマンドパレットを開き、「Open Keymap」と入力するとアクセスできます。

### macOS でのキーバインド変更例

```json
[
  {
    "context": "GitDiff",
    "bindings": {
      "cmd-alt-z": "git::RestoreAndNext"
    }
  }
]
```

### Linux / Windows でのキーバインド変更例

```json
[
  {
    "context": "GitDiff",
    "bindings": {
      "ctrl-k ctrl-r": "git::RestoreAndNext"
    }
  }
]
```

## 参考

https://github.com/zed-industries/zed/pull/50324
