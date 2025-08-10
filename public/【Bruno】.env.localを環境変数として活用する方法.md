---
title: 【Bruno】.env.localを環境変数として活用する方法
tags:
  - 'Bruno'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 基本的な.envファイルの仕組み

Brunoでは、APIキーやJWTトークンなどの機密情報を管理するために`.env`ファイルを使用できます。この`.env`ファイルは**Brunoコレクションフォルダのルート**に配置する必要があります。

### 標準的なフォルダ構造

```text
bruno-collection/
├── environments/
│   └── Local.bru
├── api-folder/
├── .env          # ← ここに配置
├── .gitignore
└── bruno.json
```

## プロジェクトの.env.localを使用する方法

Brunoで`.env.local`の値を使用するには、**シンボリックリンク**を作成します。

```shell
cd bruno-collection
ln -s ../.env.local .env
cd -
```

この操作により、以下のフォルダ構造になります。

```text
project/
├── bruno-collection/
│   ├── environments/
│   │   └── Local.bru
│   ├── api-folder/
│   ├── .env -> ../.env.local  # シンボリックリンク
│   └── bruno.json
└── .env.local                # 実際のファイル
```

### Brunoでの環境変数の使用方法

設定後、`.env.local`内の値は`process.env.<変数名>`で参照できます。

**.env.localの例**

```text
JWT_TOKEN=your_jwt_token_value
API_KEY=your_api_key_value
```

**Bruno環境ファイル（environments/Local.bru）での使用例**

```text
vars {
  baseURL: https://echo.usebruno.com
  JWT_TOKEN: {{process.env.JWT_TOKEN}}
  API_KEY: {{process.env.API_KEY}}
}
```
