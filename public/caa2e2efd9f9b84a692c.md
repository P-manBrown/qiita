---
title: 【Ruby】rbenvでバージョンが切り替えられない場合の対処法
tags:
  - Ruby
private: false
updated_at: '2024-12-29T23:55:44+09:00'
id: caa2e2efd9f9b84a692c
organization_url_name: null
slide: false
ignorePublish: false
---
# `ruby`の参照先を確認する

```
$ which ruby
/usr/bin/ruby
```

`/usr/bin/ruby`は`/.rbenv/shims/ruby`となっていなければならない。

## 参照先を変更する

`~/.zprofile`に以下の記述を追記する。

```shell:~/.zprofile
export PATH="~/.rbenv/shims:/usr/local/bin:$PATH"
eval "$(rbenv init -)"
```

以下のコマンドを実行して`~/.zprofile`を読み込む。

```terminal
source ~/.zprofile
```
