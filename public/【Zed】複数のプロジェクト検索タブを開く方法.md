---
title: 【Zed】複数のプロジェクト検索タブを開く方法
tags:
  - ZedEditor
private: false
updated_at: '2026-03-20T20:24:30+09:00'
id: 36ea0f2cff0beabddfa2
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Zedエディタのプロジェクト検索（`cmd-shift-f` / `ctrl-shift-f`）は、デフォルトでは同じペイン内に1つのタブしか開けません。
既に検索タブが開いている状態でショートカットを押すと、新しいタブが開くのではなく、既存の検索タブにフォーカスが移るだけです。

この記事では、複数のプロジェクト検索タブを同時に開く方法を紹介します。
たとえば「関数Aの使用箇所」と「関数Bの使用箇所」を並べて確認したいときに役立ちます。

## 方法1：`cmd-enter` / `ctrl-enter` で新しいタブに検索する

既存の検索タブに検索クエリを入力後、通常の `enter` の代わりに以下のショートカットを使います。

| OS | ショートカット |
|---|---|
| macOS | `cmd-enter` |
| Windows / Linux | `ctrl-enter` |

これはコマンドパレットの `project search: search in new` アクションに対応しています。

### 手順

1. `cmd-shift-f`（macOS）/ `ctrl-shift-f`（Windows / Linux）でプロジェクト検索を開く
2. 最初のキーワードを入力して `enter` で検索する
3. 2つ目のキーワードを入力する
4. `enter` の代わりに `cmd-enter`（macOS）/ `ctrl-enter`（Windows / Linux）を押す

これで、2つ目の検索結果が**新しいタブ**として開きます。

## 方法2：キーバインドを変更して常に新しいタブで開く

`cmd-shift-f` 自体を、常に新しいタブで検索を開くショートカットに変更することもできます。

`settings.json` に以下のキーバインド設定を追加します。

```json
{
  "context": "Pane",
  "bindings": {
    "cmd-shift-f": "workspace::NewSearch"
  }
}
```

WindowsやLinuxの場合は `cmd` を `ctrl` に置き換えてください。

```json
{
  "context": "Pane",
  "bindings": {
    "ctrl-shift-f": "workspace::NewSearch"
  }
}
```

この設定により、`cmd-shift-f` を押すたびに常に新しい検索タブが開くようになります。

**注意：** まだ一度も検索を実行していない未使用の検索タブが既にある場合、Zedはその既存タブにフォーカスを移します（新しいタブは開きません）。

## 参考

https://zed.dev/blog/hidden-gems-part-3#multiple-project-search-tabs
