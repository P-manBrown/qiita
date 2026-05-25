---
title: 【Zed】Markdownプレビューのフォントを変更する方法
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

Zed には Markdown プレビュー機能が搭載されており、エディタ上で Markdown を編集しながらリアルタイムにプレビューを確認できます。

このプレビューのフォントをカスタマイズする設定として、従来から本文用の `markdown_preview_font_family` が存在していましたが、Zed 1.4.0 Preview（2026年5月20日リリース）で、コードブロック・インラインコード専用の `markdown_preview_code_font_family` が新たに追加されました。

本記事では、この2つの設定を使って Markdown プレビューのフォントを自由にカスタマイズする方法を解説します。

## 関連する設定項目

Markdown プレビューのフォントに関連する設定は以下の2つです。

| 設定キー | 対象 | 未設定時のフォールバック |
|---|---|---|
| `markdown_preview_font_family` | 本文テキスト | UIフォント |
| `markdown_preview_code_font_family` | コードブロック・インラインコード | バッファフォント |

どちらの設定も **Markdown プレビューにのみ適用**されます。エージェントパネル、ホバーポップオーバー、REPL 出力などには影響しません。

## 設定方法

`Cmd + ,`（macOS）または `Ctrl + ,`（Linux/Windows）で設定ファイル（`settings.json`）を開き、以下のように追記します。

```json
{
  "markdown_preview_font_family": "Noto Serif",
  "markdown_preview_code_font_family": "Noto Sans Mono"
}
```

上記の例では、本文を `Noto Serif`（セリフ体）、コードを `Noto Sans Mono`（等幅サンスセリフ）に設定しています。本文とコードで字体が揃ったフォントペアを選ぶと、プレビューの見た目がすっきりします。

## 設定の挙動について

`markdown_preview_code_font_family` の動作は以下のとおりです。

- **未設定の場合**はバッファフォント（エディタのコードフォント）にフォールバックするため、既存のプレビュー表示は変わりません
- **フォントファミリーのみ**を上書きします。フォントのフォールバックや OpenType 機能などはバッファフォントの設定が引き続き使われます
- コードブロック・インラインコードの**両方**に適用されます

## フォント指定の例

好みや用途に応じて、以下のような組み合わせを試してみてください。

```json
{
  "markdown_preview_font_family": "Georgia",
  "markdown_preview_code_font_family": "JetBrains Mono"
}
```

```json
{
  "markdown_preview_font_family": "Hiragino Mincho ProN",
  "markdown_preview_code_font_family": "Fira Code"
}
```

フォント名はシステムにインストール済みのものを指定する必要があります。存在しないフォント名を指定した場合はフォールバックが適用されます。

## 参考

https://github.com/zed-industries/zed/pull/56744

https://zed.dev/releases/preview/1.4.0
