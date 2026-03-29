---
title: 【Zed】中央ペインにフォーカスする方法
tags:
  - ZedEditor
private: false
updated_at: '2026-03-30T00:01:55+09:00'
id: 6da38662b6f352266092
organization_url_name: null
slide: false
ignorePublish: false
---

## 背景：`editor::ToggleFocus` の問題点

以前から `editor::ToggleFocus` というアクションが存在していましたが、このアクションには使いにくい点がありました。

名前に「Toggle（切り替え）」と入っているにもかかわらず、実際にはフォーカスをエディタ側に移動するだけで、再度実行してもフォーカスが元のパネルに戻りません。つまり、トグル（行き来）の動作をしないのです。

また、ドックやパネル側にフォーカスがある状態では、期待どおりに中央ペインへフォーカスが移動しないケースもありました。

## 新アクション：`workspace::FocusCenterPane`

PR #46059 で追加された `workspace::FocusCenterPane` はこの問題を解決します。

このアクションの特徴は以下のとおりです。

- どのドックやパネルからでも、中央ペイン（最後にアクティブだったペイン）へフォーカスを移動できる
- 中央ペインがエディタだけでなく、プロジェクトDiff・ブランチDiff・ターミナル・キーマップエディタなどであっても正しく動作する
- 動作がシンプルで予測しやすい

## 設定方法

`keymap.json` に以下のようにキーバインドを追加することで、任意のキーで中央ペインにフォーカスを移動できます。

```json
[
  {
    "context": "Workspace",
    "bindings": {
      "ctrl-0": "workspace::FocusCenterPane"
    }
  }
]
```

Zedのキーマップファイルは、コマンドパレット（`cmd-shift-p`）から「zed: open keymap」を実行すると開けます。

## コマンドパレットから実行する方法

キーバインドを設定しなくても、コマンドパレットから直接実行できます。

`cmd-shift-p` でコマンドパレットを開き、`focus center pane` と入力すると `workspace: focus center pane` が候補に表示されます。

## 参考

https://github.com/zed-industries/zed/pull/46059
