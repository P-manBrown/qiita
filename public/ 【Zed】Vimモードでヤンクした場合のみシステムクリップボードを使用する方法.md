---
title: 【Zed】Vimモードでヤンクした場合のみシステムクリップボードを使用する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-01-27T23:44:59+09:00'
id: 7976bb23d6f92c1f9f00
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`settings.json`に以下を追加します。

```json
{
  "vim": {
    "use_system_clipboard": "on_yank"
  }
}
```

## use_system_clipboardの設定値

| 値          | 説明                                              |
| ----------- | ------------------------------------------------- |
| `"always"`  | 常にシステムクリップボードを使用（デフォルト）    |
| `"never"`   | システムクリップボードを使用せず、Vimレジスタのみ |
| `"on_yank"` | ヤンク時のみシステムクリップボードにコピー        |

## 参考

https://zed.dev/docs/vim#changing-vim-mode-settings
