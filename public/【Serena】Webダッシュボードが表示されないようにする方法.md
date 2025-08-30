---
title: 【Serena】Webダッシュボードが表示されないようにする方法
tags:
  - 'serena'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

Serenaの設定ファイル`~/.serena/serena_config.yml`を編集することで、webダッシュボードの動作を制御できます。

```yaml
# Webダッシュボード機能を有効/無効にする
web_dashboard: false

# Webダッシュボードの自動起動を制御（web_dashboardがtrueの場合のみ有効）
web_dashboard_open_on_launch: false
```

### `web_dashboard`
- **デフォルト値**: `true`
- **説明**: Webダッシュボード機能全体を有効または無効にします
- **設定値**:
  - `true`: ダッシュボード機能を有効にする
  - `false`: ダッシュボード機能を完全に無効にする

### `web_dashboard_open_on_launch`
- **デフォルト値**: `true`
- **説明**: Serena起動時にブラウザでダッシュボードを自動的に開くかどうかを制御します
- **前提条件**: `web_dashboard`が`true`の場合のみ有効
- **設定値**:
  - `true`: 起動時に自動的にブラウザでダッシュボードを開く
  - `false`: 自動的には開かない（手動でアクセス可能）

## 手動でのダッシュボードアクセス

`web_dashboard: true`かつ`web_dashboard_open_on_launch: false`に設定した場合、以下のURLで手動でダッシュボードにアクセスできます。

- デフォルトポート: `http://localhost:24282/dashboard/`
- 複数インスタンス実行時: `http://localhost:24283/dashboard/`、`http://localhost:24284/dashboard/`など
