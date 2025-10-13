---
title: 【Zed】ターミナルの文字列をコピーした際に選択が解除されるようにする方法
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

`settings.json`に以下を追記します。

```json
{
  "terminal": {
    "keep_selection_on_copy": false
  }
}
```

## 参考

https://zed.dev/docs/configuring-zed?highlight=keep_selection#terminal-keep-selection-on-copy
