---
title: 【Rails】debrideで未使用のメソッドを検出する方法
tags:
  - Rails
private: false
updated_at: '2024-06-26T00:02:52+09:00'
id: d0a75aa4f7b8a5e8eea4
organization_url_name: null
slide: false
ignorePublish: false
---
debrideというGemを使用することで未使用の可能性のあるメソッドを検出できます。

https://github.com/seattlerb/debride?tab=readme-ov-file

## 導入方法
Gemfileに以下を追記し、`bundle install`します。

```Gemfile：Gemfile
group :development do
  gem "debride", "~> 1.12", require: false
end
```

ターミナルで以下のコマンドを実行し、ホワイトリストを作成します。

```terminal
$ rails routes > routes.txt
$ debride_rails_whitelist routes.txt log/production.log | sort -u > whitelist.txt
$ echo up >> whitelist.txt
$ echo down >> whitelist.txt
$ echo change >> whitelist.txt
$ bundle exec debride --rails --whitelist whitelist.txt .
```

以降、`bundle exec debride --rails --whitelist whitelist.txt .
`で未使用メソッドの確認ができます。

使用されているメソッドが未使用の可能性があるメソッドとしてリストアップされた場合には、そのメソッドを`whitelist.txt`に追加します。
