---
title: 【Serena】編集ツールを無効化する方法
tags:
  - Serena
  - MCP
private: false
updated_at: '2025-09-04T21:25:59+09:00'
id: 37eb84b3cac6c62362ce
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法



### 読み取り専用モードの有効化

最も簡単で確実な方法は、プロジェクト設定で読み取り専用モードを有効化することです。

プロジェクトディレクトリ内の`.serena/project.yml`ファイルの`read_only`を`true`に変更します。

```yaml
read_only: true
```

この設定により、以下の効果が得られます。

- **すべての編集ツールが自動的に無効化**
- **ファイルの変更を防止**
- **分析・探索機能はすべて利用可能**

### 2. 特定のコマンドの無効化

より細かい制御が必要な場合は、`project.yml`の`disabled_tools`で特定のコマンドを無効化できます。

## 参考

https://github.com/oraios/serena/blob/main/README.md#shell-execution-and-editing-tools
