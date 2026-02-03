---
title: 【Zed】プロジェクトパネルのディレクトリラベルを太字にする方法
tags:
  - ZedEditor
private: false
updated_at: '2026-02-03T23:44:28+09:00'
id: 6f267fb7fbe21efe65ce
organization_url_name: null
slide: false
ignorePublish: false
---
v0.222でプロジェクトパネルのディレクトリ名を太字で表示できる機能が追加されました。

## 設定方法

`settings.json`に以下を追加します。

```json
{
  "project_panel": {
    "bold_folder_labels": true
  }
}
```

## 注意点

- この設定はデフォルトで`false`です
- ファイル名は変更されず、ディレクトリ（フォルダ）名のみが太字になります

## 参考

https://github.com/zed-industries/zed/pull/47631
