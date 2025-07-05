---
title: 【Zed】エージェントからGitHubを操作する方法
tags:
  - ZedEditor
private: false
updated_at: '2025-07-05T23:59:03+09:00'
id: dd75fd400a1716279a87
organization_url_name: null
slide: false
ignorePublish: false
---
## 拡張機能をインストール

GitHub MCP Serverという拡張機能をインストールします。

## 設定する

`settings.json`以下を追記します。

```
  "context_servers": {
    "mcp-server-github": {
      "source": "extension",
      "settings": {
        "github_personal_access_token": "アクセストークン"
      }
    }
  },

```

`repo`の権限を持つパーソナルアクセストークンを作成して記述します。

## 参考

https://github.com/LoamStudios/zed-mcp-server-github
