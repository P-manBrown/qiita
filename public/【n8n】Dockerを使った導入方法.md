---
title: 【n8n】Dockerを使った導入方法
tags:
  - n8n
private: false
updated_at: '2026-02-25T23:55:39+09:00'
id: adac81a1cfb6ff0efe87
organization_url_name: null
slide: false
ignorePublish: false
---
## 前提条件

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) インストール済み

## セットアップ

### 1. compose.yml を作成

任意のディレクトリに以下の内容で `compose.yml` を作成します。

```yaml
services:
  n8n:
    image: docker.n8n.io/n8nio/n8n
    container_name: n8n
    restart: unless-stopped
    ports:
      - "5678:5678"
    environment:
      - GENERIC_TIMEZONE=Asia/Tokyo
      - TZ=Asia/Tokyo
      - N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true
      - N8N_RUNNERS_ENABLED=true
    volumes:
      - n8n_data:/home/node/.n8n

volumes:
  n8n_data:
```

| 環境変数 | 説明 |
|---|---|
| `GENERIC_TIMEZONE` | スケジュールトリガーなどのタイムゾーン設定 |
| `TZ` | コンテナのシステムタイムゾーン |
| `N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS` | 設定ファイルのセキュアなパーミッションを強制 |
| `N8N_RUNNERS_ENABLED` | タスク実行の推奨方式（task runners）を有効化 |

### 2. 起動

```bash
docker compose up -d
```

ブラウザで http://localhost:5678 にアクセスするとセットアップ画面が表示されます。

## 停止・再起動

```bash
# 停止
docker compose down

# 再起動
docker compose restart
```

## アップデート

```bash
docker compose pull
docker compose down
docker compose up -d
```

## Webhookを使う場合

GitHub等の外部サービスからのWebhookを受け取る場合は、ローカル環境をインターネットに公開するトンネル機能が利用できます。**開発・テスト用途限定**で使用してください。

```yaml
    command: start --tunnel
```

:::note warn
`--tunnel` は本番環境での使用は推奨されていません。
:::

## 参考

https://docs.n8n.io/hosting/installation/docker/

https://github.com/n8n-io/n8n
