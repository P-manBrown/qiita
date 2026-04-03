---
title: 【Zed】プロジェクトパネルにGItステータスを表示する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-04-03T23:35:10+09:00'
id: 3eabdc2dd9c9fe9a9c94
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

デフォルトでは**無効**になっています。有効にするには `settings.json` に以下の設定を追加します。

```json
{
  "project_panel": {
    "git_status_indicator": true
  }
}
```

## 表示されるステータス一覧

ファイルの Git ステータスに応じて、ファイル名の横に以下の記号と色が表示されます。

| 記号 | 意味 | 対象 |
|------|------|------|
| `!` | コンフリクト | コンフリクトが発生しているファイル |
| `U` | 未追跡 (Untracked) | `git add` されていない新規ファイル |
| `D` | 削除済み (Deleted) | 削除されたファイル |
| `M` | 変更済み (Modified) | 編集されたファイル（ステージング前後どちらも） |
| `A` | 追加済み (Added) | ステージングされた新規ファイル |

ディレクトリの場合は記号ではなく、色付きのドットで表示されます。

## 参考

https://github.com/zed-industries/zed/pull/50216
