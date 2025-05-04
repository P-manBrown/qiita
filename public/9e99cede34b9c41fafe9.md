---
title: 【Docker】DockerHubにイメージを公開する
tags:
  - Docker
  - DockerHub
  - 初学者
private: false
updated_at: '2022-08-07T13:12:41+09:00'
id: 9e99cede34b9c41fafe9
organization_url_name: null
slide: false
ignorePublish: false
---
## リポジトリを生成する
以下の手順でDockerHubのリポジトリを生成します。  

「Create Repository」をクリックします。  
![image220807_124432.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/174ca9d2-fafe-8bd9-8c6d-5e75bad1d4ce.png)

任意のリポジトリ名を入力し「Create」をクリックします。
![image220807_124711.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/064923d4-5d47-7515-53b8-042b0c5afd6e.png)

## ローカルイメージに名前をつける
以下のいずれかの方法でローカルイメージにさきほど作成したリポジトリの名前をつけます。

* イメージをビルドする際に以下のコマンドを実行します。
```:ターミナル
$ docker build -t ユーザー名/リポジトリ名[:<tag>]
```
* 既存のローカルイメージにあらためて名前をつける
```:ターミナル
$ docker tag 既存イメージID ユーザー名/リポジトリ名[:<tag>]
```
* 変更をコミットする
```:ターミナル
$ docker commit コンテナID ユーザー名/リポジトリ名[:<tag>]
```

なお上記いずれも`[:<tag>]`を指定しない場合は`latest`となります。


## `push`する
最後に以下のコマンドを実行し、`push`します。
```:ターミナル
$ docker push ユーザー名/リポジトリ名[:<tag>]
```
