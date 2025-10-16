---
title: 【Zed】ERBファイルをフォーマットする方法
tags:
  - ZedEditor
private: false
updated_at: '2025-09-24T23:41:46+09:00'
id: 836a95deea5d6cc91aba
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
