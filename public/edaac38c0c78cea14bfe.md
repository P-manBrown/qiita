---
title: 【Next.js】Vercelにデプロイする方法
tags:
  - 初学者
  - Next.js
  - Vercel
private: false
updated_at: '2022-05-06T02:57:10+09:00'
id: edaac38c0c78cea14bfe
organization_url_name: null
slide: false
ignorePublish: false
---

## はじめに
Next.jsで作成したアプリケーションをVercelにデプロイする方法について記載します。

## Vercelにデプロイする方法
まず下記の Vercel サイトの右上の"Sign Up"からGitアカウントでサインアップしてください。

https://vercel.com/

![スクリーンショット 2022-05-06 2.34.01.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/f85586de-283c-e749-3522-0053d177540f.png)

![スクリーンショット 2022-05-06 2.35.03.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/c2db746d-8758-dc5c-ec65-8ec5fe981878.png)

サインアップが完了したら画面左側の`Import Git Repository`の入力フォームをクリックし、`Add GitHub Account`を選択してください。

![スクリーンショット 2022-05-06 2.39.36.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/926f9a2f-4fea-9863-c211-02ec1f51f4d1.png)

GitHubのページが表示されますので`Repository access`の箇所の`Only select repositories`を選択し、リポジトリを選択します。

![スクリーンショット 2022-05-06 2.44.34.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/d6083a9e-249c-16ec-ef15-d1dccf8fadf2.png)

選択したら`Save`をクリックしてください。

すると`Import Git Repository`に先ほど選択したリポジトリが表示されます。
`import`をクリックします。
![スクリーンショット 2022-05-06 2.47.16.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/75b11a0e-10be-3995-18bf-e3312f6692f5.png)


表示された画面の`Configure Project`に必要事項を入力します。
![スクリーンショット 2022-05-06 2.48.16.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/c4f577fa-5e88-9ada-66c8-007b9a4f6229.png)

入力ができたら`Deploy`をクリックします。

しばらくすると以下のような画面が表示されます。

![スクリーンショット 2022-05-06 2.54.18のコピー.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/4598cba7-6def-865a-5df4-0c5f520444fd.png)

赤枠内をクリックして正常に動作していれば完了です。


