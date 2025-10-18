---
title: 【Zed】ファイル保存時のフォーマットが動作しない問題の対処法
tags:
  - ZedEditor
private: false
updated_at: '2025-10-18T21:38:33+09:00'
id: 731733e6030987e6c851
organization_url_name: null
slide: false
ignorePublish: false
---
## 問題の概要

Zed v0.208.4にアップデート後、`format_on_save`が動作しなくなる問題が発生しました。

## 症状

- 設定で`format_on_save: "on"`を指定していてもファイル保存時にフォーマットされない
- 「deprecated settingsを修正」ボタンを押しても解決しない
- ESLintの`source.fixAll.eslint`などのcode actionのみが設定に残る

## 対処法

### パターン1: トップレベルに`formatter`設定がない場合

`"auto"`を追加します。

```json
{
  "languages": {
    "TypeScript": {
      "formatter": [
        { "code_action": "source.fixAll.eslint" },
        "auto"
      ]
    }
  }
}
```

### パターン2: トップレベルに`formatter`設定がある場合

トップレベルの値（例: `"prettier"`）を追加します。

```json
{
  "formatter": "prettier",
  "languages": {
    "TypeScript": {
      "formatter": [
        { "code_action": "source.fixAll.eslint" },
        "prettier"
      ]
    }
  }
}
```

## 公式の修正

https://github.com/zed-industries/zed/pull/40409

## 参考

https://github.com/zed-industries/zed/issues/40334
