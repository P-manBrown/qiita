---
title: 【Zed】補完メニューにシンボルを表示する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-05-19T21:47:23+09:00'
id: d422ed610a956c7649e8
organization_url_name: null
slide: false
ignorePublish: false
---

## はじめに

Zed の補完メニューには、候補の種類（関数・変数・クラスなど）を示すシンボルをテキストバッジとして表示できます。この機能は **Zed Preview 1.3.0** で追加されました。

VSCode や RustRover、Helix などの他のエディタでは補完候補の種別をアイコンや文字で視覚的に区別できますが、Zed にはこれまでその仕組みがありませんでした。今回の更新でその要望が解消されています。

## 機能の説明

補完メニューの各候補の先頭に、LSP（Language Server Protocol）が返すアイテムの種別を表す 1 文字のバッジが表示されます。バッジは現在のシンタックステーマの色に合わせて着色されます。

| 種別           | バッジ文字 |
| -------------- | ---------- |
| Function       | `f`        |
| Method         | `m`        |
| Variable       | `v`        |
| Class          | `c`        |
| Struct         | `S`        |
| Enum           | `e`        |
| Constant       | `c`        |
| Keyword        | `k`        |
| Snippet        | `s`        |
| Interface      | `i`        |
| Module         | `M`        |
| Constructor    | `C`        |
| Property       | `p`        |
| Type Parameter | `T`        |

バッジにカーソルを重ねると、種別名（例：`Function`、`Method`）のツールチップも表示されます。

## 設定方法

この機能はデフォルトで **無効** になっています。有効にするには、Zed の設定ファイル（`settings.json`）に以下を追加します。

```json
{
  "completion_menu_item_kind": "symbol"
}
```

設定ファイルは `Cmd + ,`（macOS）で開くか、コマンドパレットから `zed: open settings` を実行して開けます。

無効に戻したい場合は `"off"` を指定します。

```json
{
  "completion_menu_item_kind": "off"
}
```

## 参考

https://zed.dev/releases/preview/1.3.0

https://github.com/zed-industries/zed/pull/56396
