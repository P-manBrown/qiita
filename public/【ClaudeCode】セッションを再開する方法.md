---
title: 【ClaudeCode】セッションを再開する方法
tags:
  - ClaudeCode
private: false
updated_at: '2025-08-29T23:55:30+09:00'
id: 5cbccc4c28a80870d42f
organization_url_name: null
slide: false
ignorePublish: false
---
## 直前のセッションを再開する

`-c`または`--continue`フラグを使用すると直前のセッションを再開できます。

```bash
# インタラクティブモードで継続
claude -c

# SDKモード
claude -c -p "型エラーをチェックしてください"
```

この方法は、最後に行った会話セッションを自動的に復元します。

## 特定のセッションを再開する

特定のセッションを再開したい場合は、`-r`または`--resume`フラグを使用します。

```bash
# 特定のセッションIDで再開
claude -r "abc123" "このPRを完了させてください"

# または--resumeフラグを使用
claude --resume abc123 "バグ修正を続けてください"

# リストから選択
claude --resume
```

## 参考

https://docs.anthropic.com/en/docs/claude-code/cli-reference
