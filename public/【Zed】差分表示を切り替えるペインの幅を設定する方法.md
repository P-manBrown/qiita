---
title: 【Zed】差分表示を切り替えるペインの幅を設定する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-04-06T23:31:59+09:00'
id: 4c57abf06bb23c7cfa48
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Zedのdiff（差分）表示には、左右に並べて比較する**スプリット表示**と、変更箇所を1列にまとめた**ユニファイド表示**の2種類があります。

これまでは手動で切り替えるしかありませんでしたが、v0.231.0より、**ペインの幅に応じて自動的に表示モードを切り替える**機能が追加されました。

この記事では、その新設定 `minimum_split_diff_width` の使い方を解説します。

## diff表示の2つのモード

Zedのdiff表示には以下の2つのモードがあります。

**スプリット表示（split）**：変更前と変更後を左右に並べて比較する形式です。横幅が広い画面では見やすいですが、ペインが狭い場合は窮屈になります。

**ユニファイド表示（unified）**：変更箇所を上から順に1列で表示する形式です。縦方向にスクロールして確認するスタイルで、画面幅が狭い環境に適しています。

## minimum_split_diff_width とは

`minimum_split_diff_width` は、スプリット表示を使用する**最小のペイン幅**を「em単位」で指定する設定です。

ペインの幅がこの値を下回ると、自動的にユニファイド表示に切り替わります。ペインを広げると、また自動でスプリット表示に戻ります。`0` を設定すると自動切り替えが無効になります。

デフォルト値は `100`（em）です。

## 設定方法

`Cmd + ,`（macOS）または `Ctrl + ,`（Linux/Windows）でZedの設定ファイルを開き、以下のように記述します。

```json
{
  "minimum_split_diff_width": 150
}
```

### 設定値の例

```json
// デフォルト：150em未満でユニファイド表示に自動切り替え
{
  "minimum_split_diff_width": 150
}

// 狭いペインでもスプリット表示を維持したい場合は値を小さくする
{
  "minimum_split_diff_width": 60
}

// 自動切り替えを無効にする（常に手動で切り替える）
{
  "minimum_split_diff_width": 0
}
```

### diff_view_style との組み合わせ

`diff_view_style` はdiff表示のデフォルトモードを指定する設定です。`minimum_split_diff_width` と組み合わせると、「基本はスプリット表示だが、ペインが狭くなったら自動でユニファイドに切り替える」という挙動を実現できます。

```json
{
  "diff_view_style": "split",
  "minimum_split_diff_width": 100
}
```

`diff_view_style` を `"unified"` に設定した場合は、幅に関わらずユニファイド表示が維持されます（`minimum_split_diff_width` の自動切り替えは `"split"` モード時のみ機能します）。

## 挙動のまとめ

| ペインの幅 | diff_view_style | 実際の表示 |
|---|---|---|
| minimum_split_diff_width 以上 | split | スプリット表示 |
| minimum_split_diff_width 未満 | split | ユニファイド表示（自動切り替え） |
| いずれの幅でも | unified | ユニファイド表示 |

## 参考

https://github.com/zed-industries/zed/pull/52781
