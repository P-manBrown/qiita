---
title: 【Zed】Vimモードでwhich-keyを有効化する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-01-15T10:12:55+09:00'
id: e273ca29b0a225bafcb3
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Zed v0.219.4 以降、VimやHelixモードでwhich-keyのようなポップアップメニューが利用可能になりました。
この機能により、利用可能なキーバインドを視覚的に確認できます。

## which-keyとは

which-keyは、キー入力後に利用可能なキーバインドの一覧を表示するツールです。
Vimの[vim-which-key](https://github.com/liuchengxu/vim-which-key)プラグインと同様の機能を提供します。

## 有効化方法

Zedの設定ファイル（`settings.json`）に以下を追加します。

```json
{
  "which_key": {
    "enabled": true
  }
}
```

また、`delay_ms`でタイムアウトを設定できます。
デフォルトのタイムアウトは700msです。変更する場合は以下のように設定します。

```json
{
  "which_key": {
    "enabled": true,
    "delay_ms": 1000
  }
}
```

![screen-recording-127.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/8612ba08-2724-4b11-9468-bed24ae740d3.gif)

## 参考

https://github.com/zed-industries/zed/pull/43618
