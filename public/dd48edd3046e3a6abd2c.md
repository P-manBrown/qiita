---
title: 【Zed】特定のファイルを非表示にする方法
tags:
  - ZedEditor
private: false
updated_at: '2025-12-29T23:58:52+09:00'
id: dd48edd3046e3a6abd2c
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`settings.json`に以下のように設定します。

```json
{
  "file_scan_exclusions": [
    "**/.git",
    "**/node_modules",
    "**/.next"
  ]
}
```

除外されたファイルは以下の対象から完全に除外されます。

- ファイルスキャン
- ファイル検索
- プロジェクトツリーの表示

## デフォルト値

Zedのデフォルト設定では、以下が除外されています。
```json
"file_scan_exclusions": [
  "**/.git",
  "**/.svn",
  "**/.hg",
  "**/.jj",
  "**/CVS",
  "**/.DS_Store",
  "**/Thumbs.db",
  "**/.classpath",
  "**/.settings"
]
```

## 注意点

`file_scan_exclusions`を`settings.json`で設定すると、デフォルト値が**上書き**されます。

追加で除外したい場合は、デフォルト値も含めて記述する必要があります。
```jsonc
{
  "file_scan_exclusions": [
    // デフォルト値
    "**/.git",
    "**/.svn",
    "**/.hg",
    "**/.jj",
    "**/CVS",
    "**/.DS_Store",
    "**/Thumbs.db",
    "**/.classpath",
    "**/.settings",
    // 追加で除外
    "**/node_modules",
    "**/.next",
    "**/dist"
  ]
}
```

## 参考

https://zed.dev/docs/configuring-zed#file-scan-exclusions
