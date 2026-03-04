---
title: 【Zed】プロジェクトパネルのエラー・警告数を非表示にする方法
tags:
  - ZedEditor
private: false
updated_at: '2026-03-04T23:14:23+09:00'
id: 05dd70d22c7ee7640eb7
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

**Zed v0.226.0** から、プロジェクトパネルにエラー数・警告数を色付きバッジの表示を設定する `diagnostic_badges` が追加されました。

## 設定方法

無効にしたい場合は `~/.config/zed/settings.json` に以下を追加します。

```json
{
  "project_panel": {
    "diagnostic_badges": false
  }
}
```

## 表示のされ方

`true`の場合、ファイル名の右側にバッジが表示されます。

| バッジ色 | 内容 |
|--------|------|
| 赤 | エラー数 |
| 黄 | 警告数 |

エラーがあればファイル名も赤色、警告のみなら黄色で表示されます。エラー・警告がなければバッジは表示されません。

また、カウントは親ディレクトリにもバブルアップされるため、ディレクトリを折りたたんでいても問題のある場所をすぐに把握できます。

## 参考

https://zed.dev/releases/preview/0.226.0

https://github.com/zed-industries/zed/pull/49802
