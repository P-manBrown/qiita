---
title: 【n8n】Docker Composeでn8n + Tailscaleを構築する方法
tags:
  - tailscale
  - n8n
private: false
updated_at: '2026-02-26T23:22:41+09:00'
id: 9eedb833337c8045270c
organization_url_name: null
slide: false
ignorePublish: false
---
## 前提条件

- Docker / Docker Compose がインストール済み
- [Tailscaleアカウント](https://login.tailscale.com/)を持っている
- Tailscale管理コンソールで Auth Key を発行済み

## セットアップ手順

### 1. プロジェクトディレクトリを作成

```bash
mkdir -p ~/n8n-tailscale/tailscale_state
cd ~/n8n-tailscale
```

### 2. `.env`ファイルを作成

```dotenv
# General
SERVICE=n8n
TZ=Asia/Tokyo

# n8n
N8N_VERSION=latest
N8N_PORT=5678
TAILNET_DOMAIN=your-tailnet.ts.net   # 自分のTailnetドメインに変更

# Tailscale
TS_VERSION=latest
TS_AUTHKEY=tskey-xxxxxxxxxxxxxxxxxxxx  # 発行したAuth Keyを入力
```

> **ヒント:** Auth KeyはTailscale管理コンソールの [Settings > Keys](https://login.tailscale.com/admin/settings/keys) から発行できます。用途に応じて Reusable / Ephemeral / Tagged を選択してください。

### 3. `compose.yml`を作成

```yaml
services:
  tailscale:
    image: tailscale/tailscale:${TS_VERSION}
    container_name: tailscale-${SERVICE}
    restart: unless-stopped
    environment:
      - TS_STATE_DIR=/var/lib/tailscale
    volumes:
      - ./tailscale_state:/var/lib/tailscale
      - /dev/net/tun:/dev/net/tun
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    dns:
      - 1.1.1.1
      - 8.8.8.8
    command: >
      sh -c "
        tailscaled & sleep 8 &&
        tailscale up --authkey=${TS_AUTHKEY} --hostname=${SERVICE} &&
        echo 'Waiting for n8n to start...' &&
        while ! nc -z 127.0.0.1 ${N8N_PORT}; do sleep 2; done &&
        echo 'n8n detected, setting up Tailscale Serve...' &&
        tailscale serve --bg http://127.0.0.1:${N8N_PORT} &&
        tailscale funnel --bg http://127.0.0.1:${N8N_PORT} &&
        tail -f /dev/null
      "

  n8n:
    image: n8nio/n8n:${N8N_VERSION}
    container_name: ${SERVICE}
    restart: unless-stopped
    depends_on:
      - tailscale
    network_mode: service:tailscale
    environment:
      - GENERIC_TIMEZONE=${TZ}
      - TZ=${TZ}
      - N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true
      - N8N_RUNNERS_ENABLED=true
      - N8N_EDITOR_BASE_URL=https://${SERVICE}.${TAILNET_DOMAIN}
      - WEBHOOK_URL=https://${SERVICE}.${TAILNET_DOMAIN}/
    volumes:
      - n8n-compose_n8n_data:/home/node/.n8n

volumes:
  n8n-compose_n8n_data:
    external: true
```

### 4. 外部ボリュームを作成

```bash
docker volume create n8n-compose_n8n_data
```

### 5. スタックを起動

```bash
docker compose up -d
```

### 6. ログで動作確認

```bash
docker compose logs -f
docker exec -it tailscale-n8n tailscale status
```

成功時のログ出力例

```
n8n detected, setting up Tailscale Serve...
Serving https://n8n.your-tailnet.ts.net → http://127.0.0.1:5678
Funnel enabled: https://n8n.your-tailnet.ts.net
```

## アクセス方法

| アクセス方法                       | URL                               |
| ---------------------------------- | --------------------------------- |
| プライベート（Tailscale VPN経由）  | `https://n8n.your-tailnet.ts.net` |
| パブリック（Tailscale Funnel経由） | `https://n8n.your-tailnet.ts.net` |

## よく使うコマンド

| コマンド                                               | 説明                   |
| ------------------------------------------------------ | ---------------------- |
| `docker compose up -d`                                 | スタック起動           |
| `docker compose down`                                  | スタック停止           |
| `docker compose logs -f`                               | ログ確認               |
| `docker exec -it tailscale-n8n tailscale status`       | Tailscale接続確認      |
| `docker exec -it tailscale-n8n tailscale serve status` | Serve/Funnelの状態確認 |

## セキュリティ

Funnelを無効にしてプライベートアクセスのみにする場合は、`compose.yml`から以下の行を削除します。

```yaml
tailscale funnel --bg http://127.0.0.1:${N8N_PORT}
```

## 参考

https://docs.n8n.io

https://tailscale.com/kb/1236/serve

https://tailscale.com/kb/1223/funnel

https://docs.docker.com/compose/compose-file/

https://anime.is-a.dev/Docker-examples/n8n+tailscale.html
