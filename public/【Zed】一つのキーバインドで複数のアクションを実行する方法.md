---
title: 【Zed】一つのキーバインドで複数のアクションを実行する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-03-11T20:12:13+09:00'
id: a0857bc07abfcff61ee9
organization_url_name: null
slide: false
ignorePublish: false
---
## action::Sequence とは

Zed のキーバインドシステムには `action::Sequence` というアクションがあります。複数のアクションを一つのキーバインドにまとめて実行できる機能です。

## 基本的な書き方

`keymap.json` に以下のように記述します。

```json
{
  "bindings": {
    "cmd-alt-a": [
      "action::Sequence",
      [
        "アクション1",
        "アクション2",
        "アクション3"
      ]
    ]
  }
}
```

`action::Sequence` を指定したあと、配列で実行したいアクションを順番に並べるだけです。

## 使用例

ドックをすべて閉じ、非アクティブなタブを閉じたあと、センタードレイアウトに切り替えます。コードを書くときではなく、ドキュメントや文章を書くときに集中できる環境を一発で整えられます。

```json
"cmd-alt-a": [
  "action::Sequence",
  [
    "workspace::CloseAllDocks",
    "workspace::CloseInactiveTabsAndPanes",
    "workspace::ToggleCenteredLayout"
  ]
]
```

## 参考

https://zed.dev/blog/hidden-gems-part-3#sequence-your-actions
