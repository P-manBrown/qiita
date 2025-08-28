---
title: 【Zed】エージェントパネルでClaude Codeを使用する方法
tags:
  - 'ZedEditor'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
`acp-claude-code`を使用するとZedのエージェントパネルでClaude Codeを使用できます。

## 設定方法

`settings.json`に以下を追加します。

```json
{
  "agent_servers": {
    "claude-code": {
      "command": "npx",
      "args": ["acp-claude-code"],
      "env": {
        "ACP_PERMISSION_MODE": "acceptEdits"
      }
    }
  }
}
```

## 権限モード

- **`default`** - ファイル操作時に権限を確認
- **`acceptEdits`** - ファイル編集を自動承認（推奨）
- **`bypassPermissions`** - すべての権限をバイパス（注意）

### 動的切り替え

プロンプト内でマーカーを使用すると会話中に権限モードを変更できます。

```
[ACP:PERMISSION:ACCEPT_EDITS]
TypeScriptファイルを更新してください
```

## その他の設定例

### デバッグ有効

```json
{
  "agent_servers": {
    "claude-code": {
      "command": "npx",
      "args": ["acp-claude-code"],
      "env": {
        "ACP_DEBUG": "true",
        "ACP_PERMISSION_MODE": "acceptEdits"
      }
    }
  }
}
```

### pnpm使用

```json
{
  "agent_servers": {
    "claude-code": {
      "command": "pnpx",
      "args": ["acp-claude-code"],
      "env": {
        "ACP_PERMISSION_MODE": "acceptEdits"
      }
    }
  }
}
```

## トラブルシューティング

### 認証エラー

```bash
claude setup-token
```

### デバッグログ有効化

```bash
ACP_DEBUG=true npx acp-claude-code
```

## 参考リンク

https://zed.dev/docs/ai/external-agents#external-agents

https://zed.dev/blog/bring-your-own-agent-to-zed

https://github.com/Xuanwo/acp-claude-code
