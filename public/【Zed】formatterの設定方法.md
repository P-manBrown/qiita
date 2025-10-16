---
title: 【Zed】formatterの設定方法
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

### Language Serverを使用

```json
{
  "formatter": "language_server"
}
```

###  外部コマンドを使用

標準入力からテキストを受け取り、標準出力にフォーマット結果を出力するコマンドを指定します。

```json
{
  "formatter": {
    "external": {
      "command": "sed",
      "arguments": ["-e", "s/ *$//"]
    }
  }
}
```

#### ファイルパスのプレースホルダー

`{buffer_path}`を使うと、フォーマッタにファイルパスを渡せます（Prettierなどで有用）。

```json
{
  "formatter": {
    "external": {
      "command": "prettier",
      "arguments": ["--stdin-filepath", "{buffer_path}"]
    }
  }
}
```

**注意**: `{buffer_path}`はファイル読み込み用ではなく、フォーマッタへの情報提供用です。

### Code Actionを使用

**v0.208.4以降**

```json
{
  "formatter": [
    { "code_action": "source.fixAll.eslint" },
    { "code_action": "source.organizeImports" }
  ]
}
```

https://zed.dev/releases/stable/0.208.4

**旧形式**

```json
{
  "code_actions": {
    "source.organizeImports": true,
    "source.fixAll": true
  }
}
```

###  複数のフォーマッタを順次実行

配列で指定すると、上から順に実行されます。いずれかが失敗しても後続は実行されます。

```json
{
  "formatter": [
    { "language_server": { "name": "rust-analyzer" } },
    {
      "external": {
        "command": "sed",
        "arguments": ["-e", "s/ *$//"]
      }
    }
  ]
}
```

## 参考

https://zed.dev/docs/configuring-zed#formatter
