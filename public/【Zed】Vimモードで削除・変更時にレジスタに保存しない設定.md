---
title: 【Zed】Vimモードで削除・変更時にレジスタに保存しない設定
tags:
  - ZedEditor
private: false
updated_at: '2025-11-27T23:04:04+09:00'
id: 3992404159f3da060450
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`keymap.json`に以下の設定を追加します。

```json
{
  "context": "Editor && (vim_mode == normal || vim_mode == visual) && !VimWaiting && !menu",
  "bindings": {
    "d": ["workspace::SendKeystrokes", "\" _ d"],
    "D": ["workspace::SendKeystrokes", "\" _ D"],
    "c": ["workspace::SendKeystrokes", "\" _ c"],
    "C": ["workspace::SendKeystrokes", "\" _ C"]
  }
}
```

- この設定により、`d`、`D`、`c`、`C`の各コマンドが自動的にブラックホールレジスタ`"_`を使用するようになります
- ブラックホールレジスタに送られた内容はどこにも保存されず、クリップボードやレジスタに影響しません
- ノーマルモードとビジュアルモードで動作します

## 参考

https://github.com/zed-industries/zed/discussions/10801#discussioncomment-12348888
