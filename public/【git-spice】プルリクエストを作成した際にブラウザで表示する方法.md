---
title: 【git-spice】プルリクエストを作成した際にブラウザで表示する方法
tags:
  - git-spice
private: false
updated_at: '2025-06-02T21:46:40+09:00'
id: 1b6ac6414e98e521ecaa
organization_url_name: null
slide: false
ignorePublish: false
---

デフォルトでは`gs branch submit`などを実行してプルリクエストを作成した際にブラウザは起動しません。
作成したプルリクエストを自動でブラウザに表示したい場合には以下の設定をする必要があります。

## グローバル

次のコマンドを実行するとすべてのリポジトリで`gs branch submit`などを実行してプルリクエストを作成した際にブラウザで開かれるようになります。

```terminal
git config --global spice.submit.web true
```

## ローカル

以下のコマンドを実行すると現在のリポジトリでのみ`gs branch submit`などを実行してプルリクエストを作成した際にブラウザで開かれるようになります。

```terminal
git config --local spice.submit.web true
```

## 参考

https://abhinav.github.io/git-spice/cli/config/#spicesubmitweb
