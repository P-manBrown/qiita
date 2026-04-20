---
title: 【Zed】スクロールホイールでエディタの文字サイズを変更する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-04-20T23:25:57+09:00'
id: 33ca1281d0bd0c587d15
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Zed **v0.233.0**（Preview）から、`mouse_wheel_zoom` 設定が追加され、スクロールホイールによるフォントサイズ変更がサポートされました。

https://zed.dev/releases/preview/0.233.0

この記事では、設定方法と基本的な使い方を解説します。

## この機能でできること

`mouse_wheel_zoom` を有効にすると、次の操作でエディタのバッファフォントサイズをリアルタイムに変更できます。

- **macOS**: `Cmd` を押しながらスクロールアップ → 拡大
- **macOS**: `Cmd` を押しながらスクロールダウン → 縮小
- **Linux / Windows**: `Ctrl` を押しながらスクロールアップ → 拡大
- **Linux / Windows**: `Ctrl` を押しながらスクロールダウン → 縮小

## 設定方法

この機能はデフォルトでは無効になっています。有効にするには `settings.json` に次の設定を追加します。

```json
{
  "mouse_wheel_zoom": true
}
```

設定を保存するとすぐに反映されます。エディタの再起動は不要です。

## 設定の詳細

公式ドキュメントによると、`mouse_wheel_zoom` の定義は次のとおりです。

| 項目 | 内容 |
|------|------|
| 設定キー | `mouse_wheel_zoom` |
| デフォルト値 | `false` |
| 型 | `boolean` |
| 対応修飾キー | macOS: `Cmd`、Linux/Windows: `Ctrl` |

## 既存のフォントサイズ変更方法との違い

Zed にはこれ以前からキーボードでフォントサイズを変更する方法が用意されています。

| 操作方法 | 説明 |
|----------|------|
| `Cmd/Ctrl` + `=` | フォントサイズを拡大 |
| `Cmd/Ctrl` + `-` | フォントサイズを縮小 |
| `settings.json` の `buffer_font_size` | 設定ファイルで永続的に変更 |
| `mouse_wheel_zoom`（今回の機能） | スクロールホイールで動的に変更 |

キーボードショートカットやスクロールホイールによる変更はセッション中に反映されますが、`settings.json` に書いた `buffer_font_size` の値が基準となります。設定ファイルの値を永続的に変えたい場合は、コマンドパレットから `zed: increase buffer font size` や `zed: decrease buffer font size` などのアクションを使う方法もあります。

## 参考

https://github.com/zed-industries/zed/pull/53452
