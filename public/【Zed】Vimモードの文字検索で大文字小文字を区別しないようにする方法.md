---
title: 【Zed】Vimモードの文字検索で大文字小文字を区別しないようにする方法
tags:
  - 'ZedEditor'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`settings.json`の`vim`セクションに以下を追加します。
```json
{
  "vim": {
    "use_smartcase_find": true
  }
}
```

`use_smartcase_find`は、Vimモードの`f`と`t`モーション（文字検索）で大文字小文字を区別するかどうかを制御する設定です。

- `true`: 小文字で検索した場合は大文字小文字を区別せず、大文字が含まれる場合は区別する
- `false`（デフォルト）: 常に大文字小文字を区別する

## 設定ファイルを開く方法

1. コマンドパレット（`cmd-shift-p` / `ctrl-shift-p`）を開く
2. "zed: open settings"と入力して実行
3. `settings.json`が開く

## 動作例

`use_smartcase_find: true`の場合:

- `fa`: `a`と`A`の両方にマッチ
- `fA`: `A`のみにマッチ

## 参考

https://zed.dev/docs/vim#changing-vim-mode-settings
