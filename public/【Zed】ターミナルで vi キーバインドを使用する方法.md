---
title: 【Zed】ターミナルで vi キーバインドを使用する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-02-12T23:23:08+09:00'
id: 8fe2681599cceba92890
organization_url_name: null
slide: false
ignorePublish: false
---
## 有効化方法

ターミナル上で `Ctrl+Shift+Space` を押下すると、vi モードのオン/オフを切り替えられます。

## 使い方

vi モードが有効になると、以下のような操作が可能になります。

- `h`/`j`/`k`/`l` - カーソル移動（左/下/上/右）
- `w`/`b` - 単語単位の移動
- `0`/`$` - 行頭/行末への移動
- `v` - ビジュアルモードで選択開始
- `y` - 選択範囲のコピー

![screen-recording-141.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/674b2480-1f90-476b-864c-c8b5417b68f0.gif)

## キーマップの変更

Keymap Editorの`terminal: toggle vi mode`でキーマップを変更できます。

![screen-shot-840.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/a7da2a8c-e84c-40da-93de-7b1ee5c0b7a8.png)
