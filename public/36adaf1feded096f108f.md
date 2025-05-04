---
title: Alfred上でDeepLを使用する
tags:
  - Alfred
  - DeepL
private: false
updated_at: '2022-06-06T04:53:28+09:00'
id: 36adaf1feded096f108f
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに
以下のようにAlfred上でDeepLを使用する方法について記載します。
![スクリーンショット 2022-06-06 午前4.27.34.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/edf0b616-334a-de50-4586-b8da516536c4.png)
![スクリーンショット 2022-06-06 午前4.29.24.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/26d28052-97ca-612d-76f1-c335076b8e8d.png)

## Alfred上でDeepLを使用する方法
`DeepL-Translate`というAlfred Workflowを使用します。

https://www.packal.org/workflow/deepl-translate

上記のページからダウンロードすることができますが、こちらからダウンロードしたものだと以下のように表示され使用できませんでした。


![スクリーンショット 2022-06-06 午前4.36.58.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/c8f9ed86-9265-6f56-0463-fd6ffcd30e50.png)

なのでGitHubからダウンロードします。

https://github.com/AlexanderWillner/deepl-alfred-workflow2

ダウンロードが完了したら`Deepl-Translate.alfredworkflow`を開きます。
すると、以下のような画面が表示されます。

![スクリーンショット 2022-06-06 午前4.42.11.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/1277b098-a6e3-1eec-41f0-9f7ae464f2d4.png)

`import`をクリックします。

![スクリーンショット 2022-06-06 午前4.45.18.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/5d6d381e-f337-8d52-ff30-789043c6c861.png)

上記の画面が表示されたら`dlfr`をクリックし内容を以下の画像の通りに変更します。

![スクリーンショット 2022-06-06 午前4.43.48.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/b665876c-8469-b0c0-8f0e-9af8cbcc42c8.png)

　`dlfr`の変更点
* Keywordを任意のKeywordに変更
* FRをENに変更

以上の設定を行うことで冒頭で示した通り、Alfred上でDeepLを使用することが可能になります。
翻訳する際には文末`.`を入力する必要がありますのでご注意ください。


