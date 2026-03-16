---
title: 【Zed】選択箇所をマルチバッファで開く方法
tags:
  - ZedEditor
private: false
updated_at: '2026-03-16T23:45:04+09:00'
id: 9c9793a4f7eceaab643d
organization_url_name: null
slide: false
ignorePublish: false
---
## マルチバッファとは

Zed の「マルチバッファ」は、複数のファイルにまたがるコードをひとつのバッファにまとめて表示できる機能です。プロジェクト検索の結果やワークスペース内の選択箇所などを集約して表示できます。

## editor: open selections in multibuffer

マルチカーソルで複数箇所を選択していると、それらが多くの行に分散していることがあります。このとき、コマンドパレットから `editor: open selections in multibuffer` を実行すると、すべての選択箇所だけを集めたマルチバッファが開きます。

スクロールして一件ずつ確認する必要がなくなり、置換前の内容をまとめてレビューできます。

## 実際の使い方

1. `editor: select next` や `editor: select all matches` などで複数の箇所を選択する
2. コマンドパレット（`cmd-shift-p` / `ctrl-shift-p`）を開く
3. `open selections in multibuffer` と入力して実行する

すると、選択された箇所だけが数行間隔で並んだマルチバッファが新しいタブで開きます。

## キーバインドを設定する

頻繁に使う場合は `keymap.json` にキーバインドを登録しておくと便利です。

```json
{
  "context": "Editor",
  "bindings": {
    "cmd-alt-m": "editor::OpenSelectionsInMultibuffer"
  }
}
```

`context` を `Editor` に限定しておくことで、エディタ以外での誤作動を防げます。

## 参考

https://zed.dev/blog/hidden-gems-part-3#gather-your-selections
