---
title: 【Zed】Journalの保存先を変更する方法
tags:
  - ZedEditor
private: false
updated_at: '2025-11-07T23:40:53+09:00'
id: f2b8bfae954e56246ba8
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`settings.json`に以下の設定を追加するとJournalの保存先を変更できます。

```json
{
  "journal": {
    "path": "~/Documents/journal"
  }
}
```

- `path`: ジャーナルを保存するディレクトリのパス
  - デフォルト: `"~"`（ホームディレクトリ）
  - 指定できる値: 任意のディレクトリパス（文字列）

## 参考

https://zed.dev/docs/configuring-zed#journal
