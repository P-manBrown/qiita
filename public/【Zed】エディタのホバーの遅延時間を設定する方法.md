---
title: 【Zed】エディタのホバーの遅延時間を設定する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-04-24T00:25:29+09:00'
id: 007f7f7a3d21fea8a276
organization_url_name: null
slide: false
ignorePublish: false
---

## はじめに

Zed エディタでコードにカーソルを合わせると、型情報やドキュメントを表示するホバーポップオーバーが現れます。v0.233.5 のリリースで、このホバーポップオーバーの**表示遅延**と**非表示遅延**、そして**スティッキー動作**を細かく設定できるようになりました。

この記事では、追加された 3 つの設定項目の使い方を解説します。

## ホバーポップオーバーとは

ホバーポップオーバーとは、変数や関数にカーソルを合わせたときに表示される情報ウィンドウです。LSP（Language Server Protocol）から取得した型情報や関数のシグネチャ、ドキュメントコメントなどが表示されます。

## 追加された設定項目

今回追加された設定は以下の 3 つです。

| 設定キー | 型 | デフォルト値 | 説明 |
|---|---|---|---|
| `hover_popover_delay` | 整数（ms） | 300 | ホバー表示までの待機時間 |
| `hover_popover_sticky` | 真偽値 | true | マウスがポップオーバーに向かって移動する際にポップオーバーを維持するか |
| `hover_popover_hiding_delay` | 整数（ms） | 300 | マウスが離れてからポップオーバーが消えるまでの待機時間 |

`hover_popover_delay` は以前から存在していた設定です。今回新たに `hover_popover_sticky` と `hover_popover_hiding_delay` が追加されました。

## 各設定の詳細

### hover_popover_delay（表示遅延）

カーソルをコード上に置いてからホバーが表示されるまでの待機時間をミリ秒で指定します。この設定は `auto_signature_help` が有効な場合のシグネチャヘルプにも適用されます。

値を小さくするとすぐに表示され、大きくするとゆっくり表示されます。

### hover_popover_sticky（スティッキー動作）

`true` にすると、マウスカーソルがホバーポップオーバーに向かって移動している間、ポップオーバーが消えずに維持されます。これによりポップオーバー内のテキストをコピーしたり、リンクをクリックしたりできます。

`false` にすると、カーソルがコードから離れた瞬間にポップオーバーが即座に消えます。

### hover_popover_hiding_delay（非表示遅延）

`hover_popover_sticky` が `true` のときに有効な設定です。カーソルがコードから離れてからポップオーバーが消えるまでの待機時間をミリ秒で指定します。

この時間内にカーソルがポップオーバーに向かって移動すると、タイマーがリセットされてポップオーバーが維持されます。

## 設定方法

`settings.json` を開いて設定を追加します。コマンドパレット（`Cmd+Shift+P` / `Ctrl+Shift+P`）から `zed: open settings` を実行するか、以下のパスのファイルを直接編集します。

macOS の場合：`~/.config/zed/settings.json`

### デフォルトに近い設定（バランス重視）

```json
{
  "hover_popover_delay": 300,
  "hover_popover_sticky": true,
  "hover_popover_hiding_delay": 300
}
```

### すばやく表示・すぐ消える設定（レスポンス重視）

ホバーをなるべく素早く表示し、カーソルが離れたら即座に消したい場合は以下のようにします。

```json
{
  "hover_popover_delay": 100,
  "hover_popover_sticky": false,
  "hover_popover_hiding_delay": 0
}
```

### ポップオーバーを長めに表示する設定（じっくり読みたい場合）

ドキュメントをじっくり読みたい場合は、非表示遅延を長めに設定します。

```json
{
  "hover_popover_delay": 300,
  "hover_popover_sticky": true,
  "hover_popover_hiding_delay": 800
}
```

## VSCode からの設定インポート

VSCode の設定を Zed にインポートする場合、以下のように設定キーが対応しています。

| VSCode 設定 | Zed 設定 |
|---|---|
| `editor.hover.sticky` | `hover_popover_sticky` |
| `editor.hover.hidingDelay` | `hover_popover_hiding_delay` |

VSCode の設定をそのままインポートしても、これらの設定は自動的に Zed の対応する設定に変換されます。

## 参考

https://github.com/zed-industries/zed/pull/53504

https://zed.dev/releases/stable/0.233.5
