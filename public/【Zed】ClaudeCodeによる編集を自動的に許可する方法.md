---
title: 【Zed】ClaudeCodeによる編集を自動的に許可する方法
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

https://github.com/zed-industries/claude-code-acp/blob/d6c91b1ec12c119561c14c0b8fea4f5322677a96/src/tools.ts
