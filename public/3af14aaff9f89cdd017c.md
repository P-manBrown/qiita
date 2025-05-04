---
title: 【VSCode】JavaScriptなどのimport文をデフォルトで折りたたむ方法
tags:
  - VSCode
private: false
updated_at: '2024-07-09T23:58:10+09:00'
id: 3af14aaff9f89cdd017c
organization_url_name: null
slide: false
ignorePublish: false
---
`settings.json`に以下の設定を追記することでファイルを開いた際にimport文の部分が折り畳まれた状態になります。

```settings.json
"editor.foldingImportsByDefault": true
```
