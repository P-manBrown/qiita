---
title: 【Zed】エージェントのセッションモードのデフォルト値をaccept editsにする方法
tags:
  - ZedEditor
private: false
updated_at: '2026-01-05T23:52:01+09:00'
id: a0ef4c5eb07d08db23ea
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

### セッションモードを選択する際にcommandキーを押下する

以下の画像のリストからセッションモードを選択する際にcommandキーを押下することで初期値を切り替えられます。

![screen-shot-650.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/a2b9c5d6-47eb-482f-8f06-7cc6723a167c.png)

### settings.jsonに設定を記述する

`settings.json`に以下のように記述することでも設定できます。

```jsonc

  "agent_servers": {
    "claude": {
      "default_mode": "acceptEdits"
    }
  }

```
