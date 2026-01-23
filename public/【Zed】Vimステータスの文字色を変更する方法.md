---
title: 【Zed】Vimステータスの文字色を変更する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-01-23T23:53:23+09:00'
id: eee0e5488992441fc7c9
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`settings.json`の`theme_overrides`に以下のような設定を追記するとVimステータスの文字色を変更できます。

```json
{
  "theme_overrides": {
    "テーマ名": {
      "vim.normal.foreground": "#bb9af7",
      "vim.normal.background": "#bb9af740",
      "vim.insert.foreground": "#f7768e",
      "vim.insert.background": "#f7768e40",
      "vim.replace.foreground": "#e0af68",
      "vim.replace.background": "#e0af6840",
      "vim.visual.foreground": "#7aa2f7",
      "vim.visual.background": "#7aa2f740",
      "vim.visual_line.foreground": "#7dcfff",
      "vim.visual_line.background": "#7dcfff40",
      "vim.visual_block.foreground": "#73daca",
      "vim.visual_block.background": "#73daca40",
    },
  }
}
```

![screen-recording-132.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/24fc4536-1b4a-4b5e-b8e4-2a5daaa3676a.gif)

## 参考

https://github.com/zed-industries/zed/pull/46639
