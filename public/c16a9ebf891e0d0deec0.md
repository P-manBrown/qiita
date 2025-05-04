---
title: 【VSCode】特定のローカルブランチにコミットする際にメッセージを表示する方法
tags:
  - VSCode
  - 初学者
private: false
updated_at: '2023-04-26T00:05:09+09:00'
id: c16a9ebf891e0d0deec0
organization_url_name: null
slide: false
ignorePublish: false
---

## はじめに

VSCodeのソース管理からコミットする場合にローカルブランチを保護する方法について記載します。  
具体的にはソース管理から保護ブランチへコミットする場合に以下のメッセージが表示されるように設定します。  

![2720C7C3-C903-45FC-ABDA-3DD65D3F7AAF.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/c3a8bf6c-a3ed-de31-5480-916deaad65b2.png)


設定は非常に容易ですがVSCodeのソース管理以外からのコミットに対しては機能しません。  
他の状況にも対応するにはGit Hooksを使用するなど他の方法を採る必要があります。  

## 設定方法

VSCodeのユーザー設定画面を開きます。  

`git.branchProtection`を検索します。  

![76F7E4A0-EC37-47D9-841F-E10F50965AEB.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/4fe7a0b0-39c8-d9c4-aa5e-6b713bec21e9.png)

項目の追加をクリックして保護したいブランチ名を入力します。  

![05B65771-3937-4A9C-9048-E268DBA6986C.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/780aae82-6742-9e46-6e17-529a52b77d97.png)

これで設定は完了です。  

なおワークスペースにのみ設定を適用したい場合には設定画面のワークスペースを選択して
上記の手順を行います。  

![2B7056C5-3648-40E0-910E-7EC7BBE77533のコピー.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/17ce246c-059a-2164-7ef2-b7d3cd3fb510.png)

## 動作確認

VSCodeのソース管理から先ほど追加したブランチへ直接コミットしようとすると以下のように
表示されます。

![2720C7C3-C903-45FC-ABDA-3DD65D3F7AAF.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/c3a8bf6c-a3ed-de31-5480-916deaad65b2.png)
