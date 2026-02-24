---
title: 【Zed】パンくずリスト・アウトラインをLSPのシンボル情報で表示する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-02-25T00:26:59+09:00'
id: 8a5aa279e4f264889125
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Zedのパンくずリスト（Breadcrumbs）・アウトラインモーダル・アウトラインパネルは、デフォルトでは**Tree-sitter**の `outlines.scm` をもとにシンボルを表示しています。
v0.225.0からこれらのUIをLSP（Language Server Protocol）の `textDocument/documentSymbol` が返すシンボル情報に切り替えられるようになりました。

## Tree-sitterとLSPのシンボル表示の違い

Zedのアウトライン系UIには現在、シンボルの取得元として2つの選択肢があります。

**Tree-sitter（デフォルト）**
Zedが独自に管理する `outlines.scm` の定義にしたがって、構文ツリーからシンボルを抽出します。`mod`・`fn` などのキーワードを含む広めの範囲でシンボルが認識されるため、視覚的にわかりやすい表示になります。ただし言語ごとに `outlines.scm` が整備されている必要があります。

**LSP（オプション）**
起動中のLanguage Serverが `textDocument/documentSymbol` リクエストに応答して返すシンボル情報を使用します。LSPが対応している言語であれば利用でき、Language Serverが実際に理解しているシンボル構造をそのままアウトラインに反映できます。

## 設定方法

デフォルトでは `"document_symbols": "off"` となっており、Tree-sitterが使用されます。
LSPのシンボル情報に切り替えるには、`settings.json` の `languages` セクションで対象言語に `"document_symbols": "on"` を追加します。

```json
{
  "languages": {
    "Rust": {
      "document_symbols": "on"
    }
  }
}
```

この設定を追加すると、Rustファイルを開いた際のパンくずリスト・アウトラインモーダル・アウトラインパネルすべてで、Tree-sitterではなくLSPのシンボル情報が表示されるようになります。

複数の言語に適用したい場合は、それぞれ記述します。

```json
{
  "languages": {
    "Rust": {
      "document_symbols": "on"
    },
    "TypeScript": {
      "document_symbols": "on"
    }
  }
}
```

## 現時点での注意点

LSPのシンボル範囲はTree-sitterより**狭い**場合があります。たとえばRustの `mod` や `fn` といったキーワード部分がシンボル範囲に含まれないことがあり、パンくずリスト上でのハイライト範囲がTree-sitterのときより小さく見えることがあります。

また、現時点ではシンボルの種類（関数・クラス・変数など）に応じたアイコン表示は未実装です。将来的にはLSPが返す `kind` フィールドをもとにしたアイコン対応が計画されています。

## どちらを使うべきか

| 観点 | Tree-sitter | LSP |
|------|-------------|-----|
| デフォルト | ✅ | — |
| 追加設定 | 不要 | `"document_symbols": "on"` |
| シンボル範囲 | 広め（キーワード含む） | LSP依存（狭めのことも） |
| `outlines.scm` 未整備言語 | ❌ 表示されないことも | ✅ LSP対応なら表示可能 |
| シンボルの正確さ | Zed独自定義に依存 | Language Server依存 |

Tree-sitterの `outlines.scm` が整備されていない言語を使う場合や、Language Serverが返すシンボル構造をそのまま確認したい場合にLSPへの切り替えが有効です。

---

## 参考

https://github.com/zed-industries/zed/pull/48780

https://github.com/zed-industries/zed/issues/23095

https://github.com/zed-industries/zed/pull/48978
