---
title: Google Cloud Runでn8nをServerlessにデプロイしてみた
tags:
  - GoogleCloud
  - CloudRun
  - n8n
private: false
updated_at: '2026-03-19T20:32:16+09:00'
id: cde318fb4c6a06d3d0a1
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

n8n はオープンソースのワークフロー自動化ツールで、様々なサービスを繋いで業務を自動化できます。本記事では、Google Cloud Run を使ってサーバーレス環境に n8n をデプロイする手順を解説します。

Cloud Run を使うメリットは、サーバーの管理が不要でリクエストに応じて自動スケールする点です。使っていない時間は課金されないため、コストを抑えることができます。

なお、本記事では以下の2つのデプロイ方式を紹介します。

- **Easy mode**（簡易版）：動作確認やデモ目的向け。データは揮発性でスケールダウン時に失われる
- **Durable mode**（永続化版）：本番利用向け。PostgreSQL と Secret Manager を使用

## 前提条件

- Google Cloud プロジェクトが作成済みであること
- プロジェクトで**課金が有効**になっていること（無料枠内で動かす場合も必須）
- `gcloud` CLI がインストール済みであること

Google Cloud プロジェクトの作成方法は以下を参照してください。

https://developers.google.com/workspace/guides/create-project

## 簡単なデプロイ

### 概要

最も手軽に n8n を動かせる方法です。ただし、**データはインメモリ**に保存されるため、Cloud Run がスケールゼロになるたびにデータが失われます。デモや動作確認目的での利用に限定してください。

### 手順

Google Cloud コンソール右上のターミナルアイコン、または `G → S` のショートカットで Cloud Shell を開きます。

まず、Google Cloud にログインします（すでにログイン済みの場合はスキップ可）。

```sh
gcloud auth login
```

Cloud Run API を有効化します。

```sh
gcloud services enable run.googleapis.com
```

以下のコマンドで n8n をデプロイします。`--region` はお好みのリージョンに変更してください。

```sh
gcloud run deploy n8n \
    --image=n8nio/n8n \
    --region=us-west1 \
    --allow-unauthenticated \
    --port=5678 \
    --no-cpu-throttling \
    --memory=2Gi \
    --set-env-vars="N8N_ENDPOINT_HEALTH=health"
```

> **ポイント：** Google Cloud Run はデフォルトで `/healthz` をヘルスチェックに使用します。n8n も同じパスをデフォルトで使うため競合が発生します。`N8N_ENDPOINT_HEALTH=health` を指定することで競合を回避できます。

デプロイが完了すると、ターミナルにサービス URL が表示されます。ブラウザで開くと n8n のログイン画面が表示されます。起動直後は `n8n is starting up. Please wait` と表示される場合があるので、少し待ってからリロードしてください。

### スケールゼロを防ぐ設定（オプション）

データ消失リスクを最小化したい場合は、`--scaling=1` を追加することでインスタンス数を1に固定できます。

```sh
gcloud run deploy n8n \
    --image=n8nio/n8n \
    --region=us-west1 \
    --allow-unauthenticated \
    --port=5678 \
    --no-cpu-throttling \
    --memory=2Gi \
    --scaling=1 \
    --set-env-vars="N8N_ENDPOINT_HEALTH=health"
```

ただし、再デプロイ時にはデータが失われる点に注意してください。完全なデータ永続化には、次の Durable mode が必要です。

## 本番向けにデプロイ

PostgreSQL データベースと Secret Manager を使った、より堅牢な構成です。

### API の有効化と環境変数の設定

Cloud Shell で以下を実行します。

```sh
gcloud auth login

gcloud services enable run.googleapis.com
gcloud services enable sqladmin.googleapis.com
gcloud services enable secretmanager.googleapis.com
```

続けて、以降の手順で共通して使う環境変数を設定します。

```sh
export PROJECT_ID=your-project
export REGION=asia-northeast1  # 日本リージョンの例
```

### PostgreSQL データベースの作成

Cloud SQL に PostgreSQL インスタンスを作成します（完了まで数分かかります）。

```sh
gcloud sql instances create n8n-db \
    --database-version=POSTGRES_13 \
    --tier=db-f1-micro \
    --region=$REGION \
    --root-password="change-this-password" \
    --storage-size=10GB \
    --availability-type=ZONAL \
    --no-backup \
    --storage-type=HDD
```

インスタンス作成後、n8n 用のデータベースとユーザーを作成します。

```sh
# データベース作成
gcloud sql databases create n8n --instance=n8n-db

# ユーザー作成（パスワードは必ず変更してください）
gcloud sql users create n8n-user \
    --instance=n8n-db \
    --password="change-this-password"
```

### Secret Manager にシークレットを保存する

パスワードや暗号化キーなどの機密情報は Secret Manager に保存することを強く推奨します。

まず、データベースパスワードをファイルに書き出し、Secret Manager に登録します。

```sh
echo -n "your-db-password" > /tmp/db-password.txt

gcloud secrets create n8n-db-password \
    --data-file=/tmp/db-password.txt \
    --replication-policy="automatic"
```

次に、n8n が使う暗号化キーを生成してシークレットに登録します。

```sh
openssl rand -base64 42 > /tmp/encryption-key.txt

gcloud secrets create n8n-encryption-key \
    --data-file=/tmp/encryption-key.txt \
    --replication-policy="automatic"
```

登録が完了したら、ローカルのファイルを削除します。

```sh
rm /tmp/db-password.txt /tmp/encryption-key.txt
```

### サービスアカウントの作成と権限付与

Cloud Run サービス専用のサービスアカウントを作成し、必要最小限の権限を付与します。

```sh
# サービスアカウントの作成
gcloud iam service-accounts create n8n-service-account \
    --display-name="n8n Service Account"

# DB パスワードへのアクセス権
gcloud secrets add-iam-policy-binding n8n-db-password \
    --member="serviceAccount:n8n-service-account@$PROJECT_ID.iam.gserviceaccount.com" \
    --role="roles/secretmanager.secretAccessor"

# 暗号化キーへのアクセス権
gcloud secrets add-iam-policy-binding n8n-encryption-key \
    --member="serviceAccount:n8n-service-account@$PROJECT_ID.iam.gserviceaccount.com" \
    --role="roles/secretmanager.secretAccessor"

# Cloud SQL へのアクセス権
gcloud projects add-iam-policy-binding $PROJECT_ID \
    --member="serviceAccount:n8n-service-account@$PROJECT_ID.iam.gserviceaccount.com" \
    --role="roles/cloudsql.client"
```

### Cloud Run サービスのデプロイ

準備が整ったら、n8n を Cloud Run にデプロイします。

```sh
gcloud run deploy n8n \
    --image=n8nio/n8n:latest \
    --command="/bin/sh" \
    --args="-c,sleep 5;n8n start" \
    --region=$REGION \
    --allow-unauthenticated \
    --port=5678 \
    --memory=2Gi \
    --no-cpu-throttling \
    --set-env-vars="N8N_PORT=5678,N8N_PROTOCOL=https,N8N_ENDPOINT_HEALTH=health,DB_TYPE=postgresdb,DB_POSTGRESDB_DATABASE=n8n,DB_POSTGRESDB_USER=n8n-user,DB_POSTGRESDB_HOST=/cloudsql/$PROJECT_ID:$REGION:n8n-db,DB_POSTGRESDB_PORT=5432,DB_POSTGRESDB_SCHEMA=public,GENERIC_TIMEZONE=UTC,QUEUE_HEALTH_CHECK_ACTIVE=true" \
    --set-secrets="DB_POSTGRESDB_PASSWORD=n8n-db-password:latest,N8N_ENCRYPTION_KEY=n8n-encryption-key:latest" \
    --add-cloudsql-instances=$PROJECT_ID:$REGION:n8n-db \
    --service-account=n8n-service-account@$PROJECT_ID.iam.gserviceaccount.com
```

デプロイが完了すると、ターミナルにサービス URL が表示されます。ブラウザでアクセスすると n8n のログイン画面が開きます。

## トラブルシューティング

**`Cannot GET /` と表示される**

n8n がまだ起動中の場合に表示されます。少し時間をおいてリロードしてください。

**ヘルスチェックの競合**

`/healthz` を n8n のヘルスチェックエンドポイントとして使っている場合、Cloud Run のヘルスチェックと競合します。必ず `N8N_ENDPOINT_HEALTH=health` などの別パスを指定してください。

## （オプション）Google Workspace を n8n ツールとして使う

Gmail・Google Drive・Google Sheets などを n8n のワークフローツールとして使う場合は、OAuth の設定が必要です。

### 必要な API の有効化

```sh
gcloud services enable gmail.googleapis.com
gcloud services enable drive.googleapis.com
gcloud services enable sheets.googleapis.com
gcloud services enable docs.googleapis.com
gcloud services enable calendar-json.googleapis.com
```

### OAuth コールバック URL の設定

サービス URL を確認してから、n8n に必要な環境変数を更新します。

```sh
export SERVICE_URL="https://your-n8n-service-url.run.app"

gcloud run services update n8n \
    --region=$REGION \
    --update-env-vars="N8N_HOST=$(echo $SERVICE_URL | sed 's/https:\/\///'),WEBHOOK_URL=$SERVICE_URL,N8N_EDITOR_BASE_URL=$SERVICE_URL"
```

### OAuth クライアントの作成

Google Cloud コンソールの `https://console.cloud.google.com/auth` にアクセスし、以下の手順で設定します。

1. 「始める」ボタンをクリック（OAuth 未設定の場合）
2. アプリ名・サポートメールを入力
3. オーディエンスを選択（`Internal`：同一 Google Workspace 内のみ / `External`：外部ユーザーも対象）
4. 「クライアント」→「クライアントを作成」から Web アプリケーションを選択
5. 「承認済みの JavaScript 生成元」に n8n サービス URL を入力
6. 「承認済みのリダイレクト URI」に `https://your-n8n-url.run.app/rest/oauth2-credential/callback` を入力
7. 作成後、JSON ファイルをダウンロードしておく（クライアントシークレットは後から確認できないため）
8. 「データアクセス」で必要なスコープを追加（例：Google Sheets を使う場合は `https://googleapis.com/auth/spreadsheets` など）

設定後、n8n にログインして各サービスのクレデンシャルを追加することで、Google Workspace のサービスをワークフローツールとして利用できるようになります。

## 参考

https://docs.n8n.io/hosting/installation/server-setups/google-cloud-run/
