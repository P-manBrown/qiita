---
title: 【Git】GitHubからCSSを読み込む方法【CSS】
tags:
  - CSS
  - Git
  - GitHub
  - GithubPages
  - 初学者
private: false
updated_at: '2022-07-26T05:25:48+09:00'
id: a9669ff9b4ea5fafca52
organization_url_name: null
slide: false
ignorePublish: false
---

## リポジトリを作成する
リポジトリを作成します。
作成方法については以下のページをご参照ください。

https://docs.github.com/ja/get-started/quickstart/create-a-repo

## CSSファイルをpush
CSSファイルを作成し、`push`します。

## GitHub Pagesで公開
GitHub Pagesを使用します。
GitHubのリポジトリのSettignsページを開きます。
![image220726_050503.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/b8d9335d-cb74-3d78-d213-2098e2e93bb0.png)
下画像四角のPagesを選択します。
![image220726_050711.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/2af2e528-92fc-2df5-06b3-4cf07c0e9e42.png)
Sourceの欄で「None」が選択されていますので「main」を選択します。
選択したら「Save」をクリックします。
![image220726_050916.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/a13916d5-8ac6-bd8f-631a-79507b95be15.png)
すると下画像四角のようにURLが表示されます。
![image220726_051041.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/b420e1c7-1de6-ac0a-c694-9ce7fa949ee6.png)
表示されているURLにCSSファイルまでのパスを追加してアクセスし、内容が表示されるか確認します。
![image220726_051732.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/b081cdc3-0902-99bd-8909-9b3a645ff76e.png)

## HTMLファイルで読み込み
CSSファイルを読み込むためHTMLファイルに以下のように追記します。
```index.html
<!DOCTYPE html>
<html>
  <head>

    <link rel="stylesheet" href="CSSが表示されることを確認したURL" type="text/css">

  </head>
  <body>

  </body>
</html>
```

以上でCSSファイルが読み込まれます。
