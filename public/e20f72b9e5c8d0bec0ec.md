---
title: 【VSCode】エディタで上書きする方法
tags:
  - VSCode
private: false
updated_at: '2024-12-16T00:08:26+09:00'
id: e20f72b9e5c8d0bec0ec
organization_url_name: null
slide: false
ignorePublish: false
---
コマンドパレットで`View: Toggle Overtype/Insert Mode`を実行すると上書きモードに切り替えられます。

上書きモードでは文字を入力すると挿入されるのではなく、置き換えられます。

![overtype.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/50480473-afe4-fd77-0d90-170024d69d5f.gif)

また、`editor.overtypeOnPaste`を`true`に設定すると上書きモードにおいてペーストした際にも上書きされるようになります。
`editor.overtypeCursorStyle`で上書きモードでのカーソルを`underline`などに変更できます。

![スクリーンショット 2024-12-16 0.04.20.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/eac4ce30-4572-4345-251e-48f182b0063d.png)

