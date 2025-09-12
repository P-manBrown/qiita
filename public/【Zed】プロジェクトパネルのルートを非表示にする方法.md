---
title: 【Zed】プロジェクトパネルのルートを非表示にする方法
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

`settings.json`に以下の設定を追記するとプロジェクトパネルのルートフォルダーを非表示にできます。

```json
{
  "project_panel": {
    "hide_root": false,
  }
}

```

## 参考

https://zed.dev/docs/configuring-zed#project-panel
