---
title: 【Zed】ヤンク時の背景色を設定する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-03-10T20:43:53+09:00'
id: dcb5c490df456ff3679f
organization_url_name: null
slide: false
ignorePublish: false
---

## はじめに

Zed の Vim モードでテキストをヤンク（コピー）すると、ヤンクした範囲が一時的にハイライト表示されます。このハイライト色は以前まで設定できませんでしたが、v0.227.0で`vim.yank.background` という専用のテーマカラーが追加され、自由にカスタマイズできるようになりました。

## 変更前の挙動

この PR がマージされる前は、ヤンクのハイライト色が `editor.document_highlight.read_background` に**ハードコード**されていました。そのため、ヤンク専用の色を設定することができず、ドキュメントハイライトの色と区別がつきませんでした。

## 設定方法

`settings.json` の `theme_overrides` に `vim.yank.background` を追加するだけです。

```json
{
  "theme_overrides": {
    "テーマ名": {
      "vim.yank.background": "#カラーコード"
    }
  }
}
```

## フォールバックの仕組み

テーマが `vim.yank.background` を定義していない場合は、以前と同様に `editor.document_highlight.read_background` の色が自動的に使われます。そのため、**既存の設定を変更せずともこれまでと同じ見た目が維持されます。

## 参考

https://github.com/zed-industries/zed/pull/49517
