---
title: ' 【GitHub】タブ幅の変更方法'
tags:
  - GitHub
  - 初学者
private: false
updated_at: '2022-11-25T22:14:22+09:00'
id: ee53ad24f2aba00bbb5d
organization_url_name: null
slide: false
ignorePublish: false
---
## URL

URLに`?ts=4`などを追記することでタブ幅を変更できます。  

デフォルトは`8`です。  

- デフォルトのタブ幅
  
![スクリーンショット 2022-11-25 21.56.55.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/d0cde3bc-70fb-e8f5-a99c-044fe4c6d8e3.png)


- URLに`?ts=2`を追加
![スクリーンショット 2022-11-25 21.56.32.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/800f4248-f912-da24-eb44-4e9d01e950cf.png)


## ユーザー設定

ユーザー設定からも変更できます。  

以下のページの「Tab size preference」を任意の数字に変更します。  

https://github.com/settings/appearance

![スクリーンショット 2022-11-25 22.02.05のコピー.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/fe712323-0c71-0ae8-9389-10e4bdd9e452.png)


## EditorConfig

EditorConfigを使用することでも変更できます。  
プロジェクトルートに`.editorconfig`を作成します。  

```.editorconfig
root = true

[*]
charset = utf-8
end_of_line = lf
trim_trailing_whitespace = true
insert_final_newline = true
indent_style = space
indent_size = 2

[*.md]
trim_trailing_whitespace = false

[*.sh]
indent_style = tab

```

すると`*.sh`のタブ幅が`2`になります。  

ただし隠しファイルには反映されないようです。
