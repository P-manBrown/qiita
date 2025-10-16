---
title: 【git-spice】スタックにPRが複数存在する場合のみナビゲーションコメントをつける方法
tags:
  - git-spice
private: false
updated_at: '2025-06-03T21:24:08+09:00'
id: 9d6025bfc9b072cb5b33
organization_url_name: null
slide: false
ignorePublish: false
---

デフォルトではスタックに1つのプルリクエストしか存在しない場合でもナビゲーションコメントがつきます。

これを変更するためには以下の設定をする必要があります。

## プルリクエストが複数存在する場合のみ

プルリクエストが複数存在する場合にのみナビゲーションコメントをつける場合には以下のコマンドを実行します。

```terminal
git config --global spice.submit.navigationComment　multiple
```

現在のリポジトリのみを対象とする場合には次のコマンドを実行します。

```terminal
git config --local spice.submit.navigationComment　multiple
```

## コメントをつけない

プルリクエストにナビゲーションコメントをつけないようにするには以下のコマンドを実行します。

```terminal
git config --global spice.submit.navigationComment　false
```

現在のリポジトリのみを対象とする場合には次のコマンドを実行します。

```terminal
git config --local spice.submit.navigationComment　false
```

## 参考

https://abhinav.github.io/git-spice/cli/config/#spicesubmitnavigationcomment
