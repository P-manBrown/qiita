---
title: 【Zed】ERBファイルをフォーマットする方法
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

```jsonc
{
  "HTML/ERB": {
    "formatter": {
      "external": {
        "command": "erb-formatter",
        "arguments": ["--stdin-filename", "{buffer_path}"],
      },
    },
  },
}

```

`erb-formatter`をインストールする必要があります。

## 参考

https://zed.dev/docs/languages/ruby#formatters

https://github.com/nebulab/erb-formatter
