---
title: 【Zed】ブロックコメントを切り替える方法
tags:
  - ZedEditor
private: false
updated_at: '2026-04-23T23:51:42+09:00'
id: 48a84dde073a7b9386be
organization_url_name: null
slide: false
ignorePublish: false
---

## はじめに

Zed v0.233.5 で、**ブロックコメントのトグル**機能が追加されました。

これまでの行コメント（`//` や `#` などによる行単位のコメントアウト）に加えて、`/* ... */` のようなブロックコメントを1つのショートカットで切り替えられるようになっています。

本記事では、この新機能の使い方と、キーマップのカスタマイズ方法を紹介します。

## 行コメントとブロックコメントの違い

コメントには大きく2種類あります。

**行コメント**は1行単位でコメントアウトする方式です。

```javascript
// これは行コメントです
const x = 1; // 行末コメントも可能
```

**ブロックコメント**は複数行をまとめてコメントアウトする方式です。

```javascript
/*
  これはブロックコメントです。
  複数行をまとめて囲めます。
*/
const x = 1;
```

言語によってブロックコメントの記法は異なります。

| 言語 | ブロックコメント記法 |
|------|------------------|
| JavaScript / TypeScript | `/* ... */` |
| Ruby | `=begin ... =end` |
| HTML | `<!-- ... -->` |
| CSS | `/* ... */` |
| Rust | `/* ... */` |

## 使い方

### デフォルトのキーバインド

`editor: toggle block comment` アクションがデフォルトで以下のキーに割り当てられています。

| OS | キーバインド |
|----|------------|
| macOS | `cmd-k cmd-/` |
| Linux / Windows | `ctrl-k ctrl-/` |

### 操作手順

1. コメントアウトしたいコードを選択する
2. キーバインドを押す
3. 選択範囲がブロックコメントで囲まれる

すでにブロックコメントになっている場合は、もう一度同じキーを押すとコメントが解除されます。

### 使用例（JavaScript）

選択前：

```javascript
function greet(name) {
  console.log("Hello, " + name);
  return name;
}
```

選択してトグルした後：

```javascript
/*
function greet(name) {
  console.log("Hello, " + name);
  return name;
}
*/
```

もう一度トグルすると元に戻ります。

## コマンドパレットからの実行

キーバインドを覚えていなくても、コマンドパレットから実行できます。

1. `cmd-shift-p`（macOS）または `ctrl-shift-p`（Linux / Windows）でコマンドパレットを開く
2. `toggle block comment` と入力する
3. `editor: toggle block comment` を選択して実行

## キーバインドのカスタマイズ

デフォルトのキーバインドを変更したい場合は、`keymap.json` に設定を追加します。

Zed のメニューから `Zed > Keymap...`（macOS）または `File > Keymap...`（Linux / Windows）を開き、以下のように記述します。

```json
[
  {
    "context": "Editor",
    "bindings": {
      "cmd-/": "editor::ToggleBlockComment"
    }
  }
]
```

上記の例では `cmd-/` にブロックコメントのトグルを割り当てています。既存の行コメントトグル（`editor::ToggleComments`）と使い分けることで、用途に応じたコメント操作が快適になります。

## 行コメントとの使い分け

| 用途 | おすすめ |
|------|--------|
| 1行だけコメントアウト | 行コメント（`cmd-/`） |
| 複数行をまとめてコメントアウト | ブロックコメント（`cmd-k cmd-/`） |
| 行の途中だけコメントアウト | ブロックコメント（`/* ... */`） |
| ネストしたコメント | 言語仕様に依存するため要注意 |

## 参考

https://zed.dev/releases/stable/0.233.5

https://github.com/zed-industries/zed/pull/48752
