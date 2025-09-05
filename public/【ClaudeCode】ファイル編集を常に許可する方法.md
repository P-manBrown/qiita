---
title: 【ClaudeCode】ファイル編集を常に許可する方法
tags:
  - 'ClaudeCode'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定ファイルでのEdit権限許可

Claude Codeでファイル編集の都度確認を回避するには、設定ファイル内の `permissions` セクションの `allow` 配列に `Edit` を追加します。

### 基本的な設定方法

設定ファイル（`.claude/settings.json`、`.claude/settings.local.json`、または `~/.claude/settings.json`）に以下を記述します。

```json
{
  "permissions": {
    "allow": [
      "Edit"
    ]
  }
}
```

### パス指定による制限付き許可

特定のディレクトリやファイルのみ編集を許可する場合は、gitignore形式のパターンを使用：

```json
{
  "permissions": {
    "allow": [
      "Edit(src/**)",           // srcディレクトリ内全て
      "Edit(*.md)",             // Markdownファイルのみ
      "Edit(~/.zshrc)",         // ホームディレクトリの特定ファイル
      "Edit(//tmp/scratch.txt)" // 絶対パス指定
    ]
  }
}
```

## Permission Modesの設定

Claude Codeには権限の動作を制御する複数のPermission Modesがあります。設定ファイルの `defaultMode` で指定できます。

### 利用可能なPermission Modes

**1. default（デフォルト）**

- 各ツールの初回使用時に権限確認を要求
- 標準的な安全な動作

**2. acceptEdits**

- ファイル編集権限をセッション中自動的に受け入れ
- 編集作業の効率を大幅に向上

**3. plan**

- プランモード：ファイル分析は可能だが変更・実行は不可
- 安全にコードレビューや分析を実行

**4. bypassPermissions**

- すべての権限確認をスキップ（本番環境では非推奨）
- 最も危険だが最も効率的

### Permission Modesの設定例

```json
{
  "defaultMode": "acceptEdits"
}
```
