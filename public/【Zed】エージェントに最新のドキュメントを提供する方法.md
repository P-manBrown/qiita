---
title: 【Zed】エージェントに最新のドキュメントを提供する方法
tags:
  - ZedEditor
private: false
updated_at: '2025-07-08T23:57:40+09:00'
id: 7828ce3b5e8253edfc9f
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

「Context7 MCP Server」をインストールします。

`settings.json`に以下のとおり記述します。

```jsonc
{
  "context_server": {
    "mcp-server-context7": {
      "source": "extension",
      "enabled": true,
      "settings": {
        "default_minimum_tokens": "10000"
      }
    }
  }
}
```

これで`Write`で最新のドキュメントを参照するようになります。

## 参考

https://github.com/akbxr/zed-mcp-server-context7
