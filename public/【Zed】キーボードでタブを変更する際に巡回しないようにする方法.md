---
title: 【Zed】キーボードでタブを変更する際に巡回しないようにする方法
tags:
  - ZedEditor
private: false
updated_at: '2026-04-10T19:55:15+09:00'
id: 666510287038e0c5a961
organization_url_name: null
slide: false
ignorePublish: false
---
## デフォルトの挙動

Zedのタブ切り替えには以下のアクションが使われています。

| アクション | 説明 |
|---|---|
| `pane::ActivateNextItem` | 次のタブへ移動 |
| `pane::ActivatePreviousItem` | 前のタブへ移動 |

デフォルトでは巡回が有効になっており、タブの端まで到達すると反対側の端へ折り返します。

## 設定方法

`keymap.json` に以下のように記述することで、タブの端で止まるように変更できます。

### macOSの場合

```json
[
  {
    "bindings": {
      "cmd-shift-]": ["pane::ActivateNextItem", { "wrap_around": false }],
      "cmd-shift-[": ["pane::ActivatePreviousItem", { "wrap_around": false }]
    }
  }
]
```

`wrap_around` を `false` にすることで、最後のタブで次へ進もうとしても最初に戻らず、最後のタブにとどまるようになります。

## 参考

https://github.com/zed-industries/zed/pull/51253
