---
title: 【Zed】隠しファイルの表示・非表示を切り替える方法
tags:
  - ZedEditor
private: false
updated_at: '2025-11-15T23:51:19+09:00'
id: acf9237eb09f84c96269
organization_url_name: null
slide: false
ignorePublish: false
---
## 切り替え方法

隠しファイルの表示・非表示は以下のショートカットで切り替えられます。

- **macOS**: `Cmd + Alt + .`
- **Linux**: `Ctrl + Alt + .`
- **Windows**: `Ctrl + Alt + .`

コマンドパレットからも実行可能です。
`project panel: toggle hidden files` を実行してください。

## 隠しファイルのカスタマイズ

### デフォルト設定

デフォルトでは、ドットファイル(`.`で始まるファイル・ディレクトリ)が隠しファイルとして扱われます。

### 設定のカスタマイズ

`settings.json` で隠しファイルのパターンをカスタマイズできます。

```json
{
  "hidden_files": ["**/.*", "**/*.tmp", "**/build/**"]
}
```

**設定例**

```jsonc
{
  "hidden_files": [
    "**/.*",
    "**/*.tmp",
    "**/build/**",
    "**/node_modules/**",
    "**/*.log"
  ]
}
```
