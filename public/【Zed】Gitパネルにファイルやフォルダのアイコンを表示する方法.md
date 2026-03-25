---
title: 【Zed】Gitパネルにファイルやフォルダのアイコンを表示する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-03-25T23:32:58+09:00'
id: b628ddc90cdf229328c2
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

2026年3月16日にマージされたPR #51000により、Gitパネルでもアイコンテーマに基づいたファイルアイコン・フォルダアイコンが表示できるようになりました。

この記事では、この機能の設定方法と動作について解説します。

## 設定方法

Zedの設定ファイル（`settings.json`）に以下の設定を追加します。

### ファイルアイコンとフォルダアイコンを両方表示する

```json
{
  "git_panel": {
    "file_icons": true,
    "folder_icons": true
  }
}
```

### ファイルアイコンのみ表示する

```json
{
  "git_panel": {
    "file_icons": true
  }
}
```

### フォルダアイコンのみ表示する

```json
{
  "git_panel": {
    "folder_icons": true
  }
}
```

### アイコンをすべて非表示にする（デフォルト）

```json
{
  "git_panel": {
    "file_icons": false,
    "folder_icons": false
  }
}
```

## アイコンテーマとの連携

表示されるアイコンは、Zedに設定しているアイコンテーマが適用されます。アイコンテーマの設定は `icon_theme` で行います。

```json
{
  "icon_theme": "Catppuccin Mocha",
  "git_panel": {
    "file_icons": true,
    "folder_icons": true
  }
}
```

アイコンテーマを変更すれば、Gitパネルのアイコンもそれに合わせて切り替わります。

## 参考

https://github.com/zed-industries/zed/pull/51000
