---
title: 【Zed】保存時にESLintのエラーを自動修正する方法
tags:
  - ZedEditor
private: false
updated_at: '2024-12-31T23:54:43+09:00'
id: 0d094acd5eaa51fdfdda
organization_url_name: null
slide: false
ignorePublish: false
---
`settings.json`に以下の設定を追記すると保存時にESLintのエラーの自動修正できます。

```jsonc:settings.json
{
  "code_actions_on_format": {
    "source.fixAll.eslint": true
  }
}
```

特定の言語でのみ有効化する場合には以下のように記述します。

```jsonc:settings.json
{
  "languages": {
    "JavaScript": {
      "code_actions_on_format": {
        "source.fixAll.eslint": true
      }
    }
  }
}
```
