---
title: 【Zed】選択したディレクトリを以下を一括で折りたたむ方法
tags:
  - ZedEditor
private: false
updated_at: '2026-02-20T20:27:10+09:00'
id: dd141e00aa0e9bbe5c53
organization_url_name: null
slide: false
ignorePublish: false
---
## 概要

Zed エディタのプロジェクトパネルに、選択したディレクトリとそのすべてのサブディレクトリを一括で折りたたむアクション `project_panel::CollapseSelectedEntryAndChildren` が追加されました。

## 機能の詳細

新しいアクションを使うと、**選択中のディレクトリとその配下のすべてのサブディレクトリ**をまとめて折りたたむことができます。

## 使い方

`keymap.json` にキーバインドを追加して使用します。

以下は `h` キーに割り当てる例です。

```json
{
  "context": "(ProjectPanel && not_editing)",
  "bindings": {
    "h": "project_panel::CollapseSelectedEntryAndChildren"
  }
}
```

`context` に `ProjectPanel && not_editing` を指定することで、プロジェクトパネルにフォーカスがあり、かつ編集中でないときのみキーが有効になります。

## 参考

https://github.com/zed-industries/zed/pull/47328
