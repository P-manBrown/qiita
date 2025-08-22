## Bruno CLIとは

[Bruno](https://usebruno.com/)は、オープンソースのオフライン対応APIクライアントです。Bruno CLIは、コマンドラインからAPIコレクションを実行し、CI/CDパイプラインに統合できるツールです。

## インストール

Node.js LTSが必要です。各種パッケージマネージャーでグローバルインストールできます：

```bash
# npm
npm install -g @usebruno/cli

# yarn
yarn global add @usebruno/cli

# pnpm
pnpm install -g @usebruno/cli
```

## 基本的な使用方法

### コレクションの実行

```bash
# コレクション全体を実行
bru run

# 特定のフォルダを実行
bru run <フォルダ名>

# 特定のリクエストファイルを実行
bru run request.bru
```

### 環境設定

```bash
# 環境名を指定
bru run --env Local

# 環境ファイルを指定
bru run --env-file ./environments/local.bru

# 環境変数を動的に設定
bru run --env Local --env-var JWT_TOKEN=1234
```

## データドリブンテスト

CSVやJSONファイルを使用して反復テストが可能です：

```bash
# CSVファイルを使用
bru run --csv-file-path /path/to/data.csv

# JSONファイルを使用
bru run --json-file-path /path/to/data.json
```

## レポート生成

複数の形式でテストレポートを生成できます：

```bash
# JSONレポート
bru run --reporter-json results.json

# JUnitレポート（CI/CD向け）
bru run --reporter-junit results.xml

# HTMLレポート（人が読みやすい）
bru run --reporter-html results.html
```

## タグフィルタリング

特定のタグを持つリクエストのみ実行：

```bash
# 特定のタグを含むリクエストのみ
bru run --tags=smoke,sanity

# 特定のタグを除外
bru run --exclude-tags=skip,draft
```

## CI/CDとの統合

GitHub Actionsでの利用例：

```yaml
- name: Install Bruno CLI
  run: npm install -g @usebruno/cli

- name: Run API Tests
  run: bru run --env ci --reporter-html results.html

- name: Upload Test Results
  uses: actions/upload-artifact@v4
  with:
    name: test-results
    path: results.html
```

## その他の便利な機能

```bash
# 反復回数を指定
bru run --iteration-count=3

# リクエスト間に遅延を設定
bru run --delay 1000

# テストのみ実行
bru run --tests-only

# エラー時に停止
bru run --bail
```

## OpenAPIインポート

OpenAPIスペックからコレクションを生成：

```bash
bru import openapi --source openapi.yaml --output ./collection --collection-name "API Collection"
```

## まとめ

Bruno CLIは、APIテストの自動化において強力なツールです。CI/CDパイプラインとの統合が簡単で、豊富なレポート機能とデータドリブンテストをサポートしています。オープンソースでGit対応のため、チーム開発にも最適です。

## 参考リンク

- [Bruno公式サイト](https://usebruno.com/)
- [Bruno CLI ドキュメント](https://docs.usebruno.com/bru-cli/overview)
