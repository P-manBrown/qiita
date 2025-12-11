---
title: 【Zed】プロジェクトパネルのファイルとフォルダの並び順を変更する方法
tags:
  - ZED
private: false
updated_at: '2025-12-12T00:06:52+09:00'
id: 2825408b620ef85bcea6
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`settings.json`に以下を追加します。

```json
{
  "project_panel": {
    "sort_mode": "directories_first"
  }
}
```

`sort_mode`には以下の3つの値を指定できます。

### `"directories_first"` (デフォルト)

フォルダを先に表示し、その後にファイルを表示します。

```json
{
  "project_panel": {
    "sort_mode": "directories_first"
  }
}
```

###  `"files_first"`

ファイルを先に表示し、その後にフォルダを表示します。

```json
{
  "project_panel": {
    "sort_mode": "files_first"
  }
}
```

###  `"mixed"`

フォルダとファイルを区別せず、名前順に混在して表示します。

```json
{
  "project_panel": {
    "sort_mode": "mixed"
  }
}
```

## 参考

https://zed.dev/docs/configuring-zed#sort-mode

