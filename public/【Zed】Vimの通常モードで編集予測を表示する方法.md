---
title: 【Zed】Vimモードの通常モードで編集予測を表示する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-05-20T23:59:17+09:00'
id: 8731915c60ceb5c92bf0
organization_url_name: null
slide: false
ignorePublish: false
---

## はじめに

Zedには**編集予測（Edit Prediction）**という機能があります。コードを書いている最中に、次の編集内容をAIが予測してインラインで表示してくれる機能です。

デフォルトでは、Vimモードを使っている場合、編集予測はInsertモードとReplaceモードでのみ表示されます。Normalモードではカーソルを移動したり操作を行うことが多いため、予測が非表示になっていました。

Zed Preview 1.3.0（PR #55956）で、Normalモードでも編集予測を表示できる新しい設定 `vim.show_edit_predictions_in_normal_mode` が追加されました。

## 編集予測とは

編集予測は、現在のカーソル位置に対してAIが「次にどんな編集をするか」を予測し、薄いテキストとしてインライン表示する機能です。

Zedが独自に開発したモデル **Zeta** をはじめ、GitHub Copilot や Codestral など複数のプロバイダーに対応しています。デフォルトでは `tab` キーで予測を確定できます。

## 設定方法

`settings.json` を開き（`cmd+,` または `ctrl+,`）、以下の設定を追加します。

```json
{
  "vim": {
    "show_edit_predictions_in_normal_mode": true
  }
}
```

デフォルト値は `false` です。`true` にすると、VimのNormalモードおよびHelixのNormalモードで編集予測が表示されるようになります。

## デフォルト設定との比較

| モード  | デフォルト（false） | 有効時（true） |
| ------- | ------------------- | -------------- |
| Insert  | ✅ 表示              | ✅ 表示         |
| Replace | ✅ 表示              | ✅ 表示         |
| Normal  | ❌ 非表示            | ✅ 表示         |
| Visual  | ❌ 非表示            | ❌ 非表示       |

## GUIから設定する方法

Settings UIからも変更できます。`zed: open settings` コマンドでSettings画面を開き、**Vim** セクションにある **Show Edit Predictions in Normal Mode** というトグルをオンにするだけです。

## 参考

https://zed.dev/releases/preview/1.3.0

https://github.com/zed-industries/zed/pull/55956
