---
title: 【VSCode】文字エンコードを自動判別する方法
tags:
  - VSCode
  - 初学者
private: false
updated_at: '2023-05-13T23:59:18+09:00'
id: beb4dc864c4c2a3cf0e3
organization_url_name: null
slide: false
ignorePublish: false
---
## 文字エンコードを自動判別する方法

次の手順で設定することでファイルを開いた際に文字エンコードを自動判別できるようになります。

### ユーザー設定を開く

`command` + `shift` + `P`を入力してコマンドパレットを開きます。

`Open User Settings`と入力しユーザー設定を開きます。

![スクリーンショット 2023-05-13 23.53.03.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/160d17e2-4ebf-3f5a-f6ee-2a0a3f7d9857.png)

## 設定する

ユーザー設定の検索窓に`Files:Auto Guess Encoding`と入力して検索します。

ヒットした設定にチェックをつけます。

![スクリーンショット 2023-05-13 23.56.23.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/1aa655f5-5489-e552-4816-72a8e177fa30.png)

以上でファイルをVSCodeでファイルを開いた際に文字エンコードを自動で判別してくれるようになります。
