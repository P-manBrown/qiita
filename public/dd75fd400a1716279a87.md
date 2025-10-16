---
title: 【Zed】エージェントからGitHubを操作する方法
tags:
  - ZedEditor
private: false
updated_at: '2025-07-06T00:06:09+09:00'
id: dd75fd400a1716279a87
organization_url_name: null
slide: false
ignorePublish: false
---
## 拡張機能をインストール

GitHub MCP Serverという拡張機能をインストールします。

## 設定する

`settings.json`以下を追記します。

```jsonc
{
  "context_servers": {
    "mcp-server-github": {
      "source": "extension",
      "settings": {
        "github_personal_access_token": "パーソナルアクセストークン"
      }
    }
  },
}
```

`repo`の権限を持つパーソナルアクセストークンを作成して記述します。

## `Ask`で使用する場合

エージェントプロファイルの設定で`Ask`を選択し、`Configure MCP Tools`で使用したいツールにチェックをつける必要があります。

![screen-shot-465.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/be182da9-085f-4bf5-99da-0c237b2986d8.png)


## 参考

https://github.com/LoamStudios/zed-mcp-server-github
