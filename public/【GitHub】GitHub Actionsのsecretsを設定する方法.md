---
title: 【GitHub】GitHub Actionsのsecretsを設定する方法
tags:
  - 'GitHub'
  - 'GitHubActions'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

## 設定方法

1. リポジトリの「Settings」をクリック
2. 「Secrets and variables > Actions」をクリック
3. 「New repository secret」をクリック

![4B143EF9-D87B-4243-B34C-BA15C3812F2B.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/ee71dd82-44b1-4217-8dc1-cfa65c278190.png)

4. secretの名称を入力
5. secretの値を入力
6. 「Add secret」をクリック

![D992063C-30C6-4D1B-89B6-0EAA9B38634C.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/d92fd0f7-d3b6-4138-bdb8-f1b50302a853.png)

## secretsを使用する

設定したsecretsを使用するには`${{ secrets.シークレット名 }}`のようにします。

```yaml
steps:
  - name: Hello world action
    with: # Set the secret as an input
      super_secret: ${{ secrets.SAMPLE_SECRET }}
    env: # Or as an environment variable
      super_secret: ${{ secrets.SAMPLE_SECRET }}
```

## 参考

https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions#creating-secrets-for-a-repository
