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
## 設定方法

Zed の設定ファイル（`settings.json`）に以下を追加します。

```json
{
  "git_panel": {
    "starts_open": true
  }
}
```

`starts_open` に `true` を設定すると、パネルの状態が保存されていない新しいワークスペースで Git パネルが自動的に開きます。`false`（デフォルト値）の場合は、従来通り閉じた状態でワークスペースが起動します。

## 「パネルの状態が保存されていない」とは

この設定が有効になるのは、**保存済みのパネル状態がないワークスペース**が対象です。

Zed はワークスペースごとにパネルの開閉状態を記憶しています。たとえば、一度 Git パネルを手動で閉じたワークスペースは「閉じている」という状態が保存されるため、`starts_open: true` であっても次回起動時は閉じた状態になります。

`starts_open` が効くのは、主に以下のようなケースです。

- 新しいフォルダを初めて Zed で開いたとき
- パネル状態がまだ記録されていないワークスペース

## 参考

https://github.com/zed-industries/zed/pull/51601
