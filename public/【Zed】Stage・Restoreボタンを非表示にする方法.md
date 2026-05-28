---
title: 【Zed】Stage・Restoreボタンを非表示にする方法
tags:
  - ZedEditor
private: false
updated_at: '2026-05-27T23:06:09+09:00'
id: 82634cc45b3a175e4ccf
organization_url_name: null
slide: false
ignorePublish: false
---

## はじめに

Zed v1.4.0（Preview）で、差分ハンク（diff hunk）上に表示される **Stage** / **Restore** ボタンを非表示にできる設定 `git.show_stage_restore_buttons` が追加されました。

長い行や狭いビューポートでは、これらのボタンがコードに重なって見づらくなることがあります。本記事では、その設定方法を紹介します。

## Stage/Restoreボタンとは

Zedでファイルを編集してGitの差分が生じると、各差分ハンクの右端に **Stage**（またはUnstage）と **Restore** というボタンが表示されます。これらはクリックするだけで変更をステージングしたり元に戻したりできる便利な機能です。

一方、1行が長いコードを書いているときや画面幅が狭いときは、ボタンがコードに重なって視認性を下げてしまう場面があります。

## 設定方法

`settings.json` に以下を追加します。

```json
{
  "git": {
    "show_stage_restore_buttons": false
  }
}
```

`false` に設定するとボタンが非表示になります。デフォルトは `true`（表示）です。

## ボタンなしでStage/Restoreを行う方法

ボタンを非表示にした場合でも、キーボードショートカットやコマンドパレットから同じ操作を実行できます。

| 操作 | コマンド |
|------|---------|
| ハンクをステージ / アンステージ | `git: toggle staged` |
| ハンクを元に戻す | `git: restore hunk` |

コマンドパレット（`Cmd+Shift+P`）から上記のコマンドを検索して実行できます。

## 参考

https://zed.dev/releases/preview/1.4.0

https://github.com/zed-industries/zed/pull/56740
