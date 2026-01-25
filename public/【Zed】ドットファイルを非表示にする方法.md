---
title: 【Zed】プロジェクトパネルのドットファイルを非表示にする方法
tags:
  - ZedEditor
private: false
updated_at: '2026-01-25T23:58:48+09:00'
id: 7bb7762e00ada90e1ca0
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法
`settings.json`に以下の設定を記述するとプロジェクトパネルにドットファイルが表示されなくなります。

```jsonc
{
  "project_panel": {
    "hide_hidden": true,
  },
}
```

## 切り替え方法

ドットファイルの表示・非表示は以下のショートカットで切り替えられます。

- **macOS**: `Cmd + Alt + .`
- **Linux**: `Ctrl + Alt + .`
- **Windows**: `Ctrl + Alt + .`

コマンドパレットからも実行可能です。
`project panel: toggle hidden files` を実行してください。
