---
title: 【ClaudeCode】優先応答言語を設定する方法
tags:
  - ClaudeCode
private: false
updated_at: '2026-01-15T19:45:39+09:00'
id: 1004e4cfdf8484a8dd7d
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Claude Code 2.1.0から、Claudeの応答言語を設定できる機能が追加されました。この設定により、コンパクト化された後に急に英語で応答し始めるという問題を解決できます。

## 設定方法

`~/.claude/settings.json`または`.claude/settings.json`に以下を追加します。

```json
{
  "language": "japanese"
}
```

## 設定ファイルの配置場所

### ユーザー設定

- 場所: `~/.claude/settings.json`
- すべてのプロジェクトに適用されます。

### プロジェクト設定

- 場所: `.claude/settings.json`
- 特定のプロジェクトのみに適用され、チームで共有できます。

### ローカル設定

- 場所: `.claude/settings.local.json`
- 個人的な設定で、gitにコミットされません。

## 参考

https://code.claude.com/docs/en/settings#available-settings

https://claudelog.com/claude-code-changelog/#v210
