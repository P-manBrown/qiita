---
title: 【Zed】新しいワークスペースで、Git パネルが自動的に開くようにする方法
tags:
  - ZedEditor
  - Git
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

Zed には、新しいワークスペースを開いたときに Git パネルを自動的に表示する設定があります。この記事では、`git_panel.starts_open` 設定の使い方を解説します。

## この機能について

Zed の Git パネルは、変更ファイルの確認やコミットなどの Git 操作をエディタ内で行えるパネルです。

デフォルトでは、新しいワークスペースを開いても Git パネルは閉じた状態になっています。毎回手動で開くのが手間に感じる場合は、`git_panel.starts_open` を使うと、ワークスペースを開いた時点から Git パネルが自動で表示されるようになります。

この機能は、すでに存在する `project_panel.starts_open` と同じパターンで実装されており、2026年3月18日に本家リポジトリへマージされました。

https://github.com/zed-industries/zed/pull/51601

## 設定方法

Zed の設定ファイル（`settings.json`）に以下を追加します。

```json
{
  "git_panel": {
    "starts_open": true
  }
}
```

設定ファイルは、コマンドパレット（`Cmd+Shift+P` / `Ctrl+Shift+P`）から `zed: open settings` を実行すると開けます。

`starts_open` に `true` を設定すると、パネルの状態が保存されていない新しいワークスペースで Git パネルが自動的に開きます。`false`（デフォルト値）の場合は、従来通り閉じた状態でワークスペースが起動します。

## 「パネルの状態が保存されていない」とは

この設定が有効になるのは、**保存済みのパネル状態がないワークスペース**が対象です。

Zed はワークスペースごとにパネルの開閉状態を記憶しています。たとえば、一度 Git パネルを手動で閉じたワークスペースは「閉じている」という状態が保存されるため、`starts_open: true` であっても次回起動時は閉じた状態になります。

`starts_open` が効くのは、主に以下のようなケースです。

- 新しいフォルダを初めて Zed で開いたとき
- パネル状態がまだ記録されていないワークスペース

## project_panel との対称性

Zed には `project_panel`（ファイルツリー）にも同様の設定があります。

```json
{
  "project_panel": {
    "starts_open": true
  }
}
```

`git_panel.starts_open` は、この `project_panel.starts_open` と同じ仕組みで動作します。両方を組み合わせると、ワークスペースを開いた瞬間からファイルツリーと Git パネルを両方表示させることができます。

```json
{
  "project_panel": {
    "starts_open": true
  },
  "git_panel": {
    "starts_open": true
  }
}
```

## まとめ

`git_panel.starts_open` を `true` にすると、新しいワークスペースで Git パネルが自動的に開くようになります。Git を使った開発が中心の場合は、この設定を有効にしておくと毎回パネルを手動で開く手間が省けて便利です。デフォルトは `false` なので、既存の動作には影響しません。
