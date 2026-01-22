---
title: 【Zed】エージェントパネルに処理時間などを表示する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-01-22T23:54:59+09:00'
id: f891400e374f8cec4b98
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

エージェントの統計情報を表示するには、Zedの設定ファイルに以下を追加します。
```json
{
  "agent": {
  	"show_turn_stats": true
  }
}
```

デフォルトでは`false`に設定されているため、明示的に有効化する必要があります。

## 表示される情報

この機能を有効にすると、エージェントパネルに以下の情報が表示されます。

- **処理時間**: エージェントがメッセージを処理するのにかかった時間
- （**トークン数**: 使用したトークンの数）

![screen-shot-817.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/a0466dae-3a73-4bce-b8a0-3af4e924e2cf.png)

## 参考

https://github.com/zed-industries/zed/pull/46390
