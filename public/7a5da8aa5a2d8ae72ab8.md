---
title: 【Git】submoduleの追加と削除
tags:
  - Git
  - GitHub
  - 初学者
private: false
updated_at: '2023-02-07T23:45:11+09:00'
id: 7a5da8aa5a2d8ae72ab8
organization_url_name: null
slide: false
ignorePublish: false
---
## 追加

リポジトリにサブモジュールを追加するには次のコマンドを実行します。

```terminal
git submodule add サブモジュールのリポジトリURL サブモジュールのディレクトリ
```

```
git submodule add https://github.com/user/sample-submodule.git sample/sample-submdules
```

上記を実行した後に`.gitmodules`ファイルが作成され`sample/sample-submodules`の中に`https://github.com/user/sample-submodule.git`の内容がcloneされます。

## 削除

削除する際には次の手順を実行します。

```terminal
$ git submodule                           
 4a3a41a70aeeb503f56cf7ba486235b6fao28af2 sample/sample-submodules (4a3a41a)
$ git submodule deinit sample/sample-submodules
$ git rm -f sample/sample-submodules
```
