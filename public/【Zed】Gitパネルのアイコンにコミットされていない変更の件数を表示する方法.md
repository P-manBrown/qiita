---
title: 【Zed】Gitパネルのアイコンにコミットされていない変更の件数を表示する方法
tags:
  - Git
  - ZedEditor
private: false
updated_at: '2026-03-27T01:08:54+09:00'
id: 14e856215c3b326612c3
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Zed 0.229.0 から、サイドバーの Git パネルアイコンにコミットされていない変更の件数をバッジ表示できるようになりました。

VS Code の「ソース管理」アイコンに表示されるカウントバッジと同様の機能で、Git パネルを開かなくても未コミットの変更がひと目でわかるようになります。

ただし、**デフォルトでは無効**になっているため、設定を有効化する必要があります。本記事ではその手順を解説します。

## 有効化の方法

`settings.json` に以下の設定を追加します。

設定ファイルは、コマンドパレット（`Cmd+Shift+P` / `Ctrl+Shift+P`）で `zed: open settings` を実行すると開けます。

```json
{
  "git_panel": {
    "show_count_badge": true
  }
}
```

設定を保存すると即座に反映されます。Git リポジトリ内でコミットされていない変更がある場合、サイドバーの Git アイコンの右上に数字が表示されます。

![screen-shot-1023.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/e40b1b60-0807-45f7-b94f-1f53eaf77281.png)

## 動作の仕様

| 状態 | バッジの表示 |
|------|-------------|
| 未コミットの変更が 0 件 | 非表示 |
| 未コミットの変更が 1〜99 件 | 件数を表示 |
| 未コミットの変更が 100 件以上 | `99+` を表示 |
| Git パネルが開いている | 非表示 |

バッジが非表示になる条件は「未コミットの変更が 0 件のとき」と「Git パネルが開いているとき」の 2 つです。パネルを閉じると再び表示されます。

## 参考

https://zed.dev/releases/stable/0.229.0

https://github.com/zed-industries/zed/pull/49624
