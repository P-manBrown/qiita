---
title: 【Zed】コミットエディタを展開する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-05-18T23:35:56+09:00'
id: aa638ea1078fbb873e5e
organization_url_name: null
slide: false
ignorePublish: false
---
## `git::ExpandCommitEditor`と`git::ToggleFillCommitEditor`の違い

Zed にはコミットエディタを広げるアクションが 2 種類あります。

| アクション                    | 挙動                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| `git::ExpandCommitEditor`     | モーダル（別ウィンドウ）を開く。エディタ中央に表示されるため、diff と同時に見づらい |
| `git::ToggleFillCommitEditor` | Git パネル内でエディタを縦方向に最大展開する。変更ファイル一覧は非表示になり、フッターのみ残る |

`ToggleFillCommitEditor` の場合、モーダルを使わずにパネル内で展開するため、横に `git: branch diff` を表示しながら作業できるのが大きなメリットです。

## デフォルトキーバインド

OS ごとのデフォルトキーバインドは以下のとおりです。

| OS      | `ExpandCommitEditor` | `ToggleFillCommitEditor` |
| ------- | -------------------- | ------------------------ |
| macOS   | `shift-escape`       | `alt-shift-escape`       |
| Linux   | `shift-escape`       | `alt-shift-escape`       |
| Windows | `shift-escape`       | `alt-shift-escape`       |

キーバインドはいずれも Git パネルのコミットエディタにフォーカスがある状態で使用します。

## GUI から操作する方法

キーバインドを使わずにボタンで操作することもできます。Git パネルのコミットエディタ右上に 2 つのアイコンボタンが表示されています。

- **MaximizeAlt アイコン**：`Open Commit Modal`（モーダルを開く）
- **Maximize / Minimize アイコン**：`Expand Commit Editor` / `Collapse Commit Editor`（パネル内で展開・折りたたむ）

展開中は "Collapse Commit Editor"、折りたたみ中は "Expand Commit Editor" というツールチップが表示されます。

## keymap.json でカスタマイズする方法

デフォルトのキーバインドを変更したい場合は `keymap.json` を編集します。

コマンドパレット（`cmd-shift-p` / `ctrl-shift-p`）から `zed: open keymap` を実行してファイルを開き、以下のように記述します。

```json
[
  {
    "context": "GitPanel",
    "bindings": {
      "ctrl-e": "git::ToggleFillCommitEditor"
    }
  }
]
```

上の例では `ctrl-e` に `ToggleFillCommitEditor` を割り当てています。`context` に `GitPanel` を指定することで、Git パネルにフォーカスがある場合のみ有効になります。

## 参考

https://github.com/zed-industries/zed/pull/55043
