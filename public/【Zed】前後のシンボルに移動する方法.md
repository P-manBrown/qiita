---
title: 【Zed】前後のシンボルに移動する方法
tags:
  - ZedEditor
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Zed にアウトライン上の前後のシンボルへジャンプする2つのアクションが追加されました。

- `editor::GoToNextSymbol`（次のシンボルへ移動）
- `editor::GoToPreviousSymbol`（前のシンボルへ移動）

コードを読み解きながら関数やクラスを順番に追いたいとき、マウスを使わずキーボードだけでシンボル間を素早く移動できるようになります。

参考 PR：

https://github.com/zed-industries/zed/pull/50777

## シンボルとは

ここでいう「シンボル」とは、エディタのアウトラインに表示される要素のことです。具体的には次のようなものが該当します。

- Rust の `fn`（関数）や `struct`（構造体）
- Python の `class` や `def`
- Markdown の見出し（`#`、`##` など）

アウトラインは Tree-sitter または LSP（Language Server Protocol）のどちらかから取得されます。どちらを使うかはエディタの設定に依存しますが、どちらの場合でも同じアクションで動作します。

## 使い方

### コマンドパレットから実行する

`Cmd+Shift+P`（macOS）または `Ctrl+Shift+P`（Linux/Windows）でコマンドパレットを開き、`Go To Next Symbol` または `Go To Previous Symbol` と入力して実行します。

### キーバインドを設定する

毎回コマンドパレットから実行するのは手間なので、キーバインドを設定しておくと便利です。`Cmd+,` でキーバインド設定ファイルを開き、以下のように追記します。

```json
[
  {
    "context": "Editor",
    "bindings": {
      "alt-down": "editor::GoToNextSymbol",
      "alt-up": "editor::GoToPreviousSymbol"
    }
  }
]
```

この設定では `Alt+↓` で次のシンボル、`Alt+↑` で前のシンボルへジャンプします。任意のキーに変更して構いません。

## 動作の詳細

### 移動先の決まり方

カーソル位置から見て、移動方向にある最も近いシンボルの先頭へカーソルが移動します。カーソルがすでにあるシンボルの範囲内にいる場合、そのシンボルはスキップされ、次のシンボルへ移動します。

### 空白行（デッドゾーン）にいるとき

どのシンボルの範囲にも属さない空白行にカーソルがある場合でも、移動方向にある最も近いシンボルへ正しくジャンプします。以下はそのイメージです。

```
fn foo() {
    // foo fn
}

// ← ここ（デッドゾーン）にカーソルがあっても…

fn bar() {
    // bar fn
}
```

上記の状態で `GoToNextSymbol` を実行すると、`fn bar()` の先頭へ移動します。`GoToPreviousSymbol` であれば `fn foo()` の先頭へ移動します。

### 先頭・末尾のシンボルでの動作

先頭のシンボルにいる状態で `GoToPreviousSymbol` を実行してもカーソルは動きません。同様に、末尾のシンボルで `GoToNextSymbol` を実行してもカーソルはそのままです。ループして反対端へ戻る動作はしません。

## マルチバッファでの動作

このアクションはシングルバッファ（通常のファイル編集）のみを対象としています。検索結果などのマルチバッファ表示では動作しません。

## 参考

https://github.com/zed-industries/zed/pull/50777
