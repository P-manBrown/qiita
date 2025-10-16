---
title: 【Zed】ClaudeCodeによる編集を自動的に許可する方法
tags:
  - ZedEditor
private: false
updated_at: '2025-09-10T22:23:11+09:00'
id: d9366e95bb05cd4cd131
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`.claude/settings.json`に以下を記述するとClaudeCodeによって編集されるたびに許可を求められなくなります。

```json
{
  "permissions": {
    "allow": [
      "mcp__acp__edit",
      "mcp__acp__multi-edit",
      "mcp__acp__write"
    ],
    "deny": [],
    "ask": []
  }
}

```

## 参考

https://github.com/zed-industries/claude-code-acp
