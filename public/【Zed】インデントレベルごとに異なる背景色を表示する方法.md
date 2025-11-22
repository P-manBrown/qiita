---
title: 【Zed】インデントレベルごとに異なる背景色を表示する方法
tags:
  - ZedEditor
private: false
updated_at: '2025-11-22T22:23:14+09:00'
id: 8c9530567dff1a56f588
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`settings.json`ファイルを開き、以下の設定を追記します。

```jsonc
{
  "indent_guides": {
    "enabled": true,
    "background_coloring": "indent_aware"
  }
}
```

- `background_coloring`

  - `"disabled"`: 背景色なし（デフォルト）

  - `"indent_aware"`: インデントレベルごとに異なる背景色を適用


## インデントガイドに関するその他の設定

```jsonc
{
  "indent_guides": {
    "enabled": true,
    "line_width": 1,
    "active_line_width": 1,
    "coloring": "indent_aware",
    "background_coloring": "indent_aware"
  }
}
```

- `coloring`: インデントガイドの線の色を設定
  - `"fixed"`: 固定色
  - `"indent_aware"`: インデントレベルごとに異なる色
- `line_width`: インデントガイドの線の太さ
- `active_line_width`: アクティブな行のインデントガイドの線の太さ

## 参考

https://zed.dev/docs/configuring-zed#indent-guides

