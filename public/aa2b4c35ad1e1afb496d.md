---
title: 【Bruno】GitHub Actionsでコマンドを実行する方法
tags:
  - Bruno
private: false
updated_at: '2025-08-24T22:16:21+09:00'
id: aa2b4c35ad1e1afb496d
organization_url_name: null
slide: false
ignorePublish: false
---
## プロジェクト構造

```txt
project/
├── .github/workflows/api-tests.yml
├── collections/
│   └── authentication/
├── environments/
│   ├── development.bru
│   └── ci.bru
└── bruno.json
```

## GitHub Actionsワークフローの作成

`.github/workflows/api-tests.yml`ファイルを作成します。

```yaml
name: API Tests

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout code
      uses: actions/checkout@v4
      
    - name: Setup Node.js
      uses: actions/setup-node@v4
      with:
        node-version: '20'
        
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

## ワークフローの実行

1. **ファイルをコミット**

```bash
git add .github/workflows/api-tests.yml
git commit -m "Add GitHub Actions workflow for API testing"
git push origin main
```

1. **実行確認**

- GitHubリポジトリの「Actions」タブで実行状況を確認
- 完了後、「Artifacts」から`results.html`をダウンロードしてレポートを確認

## 参考

https://docs.usebruno.com/bru-cli/gitHubCLI

https://docs.github.com/en/actions
