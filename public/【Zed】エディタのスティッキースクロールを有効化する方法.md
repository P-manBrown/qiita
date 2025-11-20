---
title: 【Zed】エディタのスティッキースクロールを有効化する方法
tags:
  - ZedEditor
private: false
updated_at: '2025-11-20T23:51:44+09:00'
id: 4d0c245106dd58be4860
organization_url_name: null
slide: false
ignorePublish: false
---
## 対応バージョン

Zed v0.213.3（2024年11月19日リリース）以降

## 設定方法

`settings.json`に以下を追記します。

```jsonc
{
  "sticky_scroll": {
    "enabled": true
  }
}
```

## 参考

https://zed.dev/releases/stable/0.213.3
