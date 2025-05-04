---
title: 【Bundler】Gemのバージョンを指定する方法
tags:
  - Gem
  - Bundler
  - 初学者
private: false
updated_at: '2022-12-03T23:39:51+09:00'
id: baefa2b051f4d2b0fe37
organization_url_name: null
slide: false
ignorePublish: false
---
## Gemのバージョン指定方法

`Gemfile`に以下のように記述することでGemのバージョンを指定できます。  

```Gemfile
gem "Gem名", "バージョン"
```

バージョン指定は以下のような指定ができます。  

| 指定方法               | 説明                                       |
| ---------------------- | ------------------------------------------ |
| '1.0.0'                | v1.0.0固定                                 |
| '>= 1.0.0'             | v1.0.0以上                                 |
| '>= 1.0.0' , '< 2.0.0' | v1.0.0以上v2.0.0未満                       |
| '~> 1.0.0'             | v1.0.0以上でマイナーバージョンが変わらない |
| '~> 1.0'               | v1.0.0以上でメジャーバージョンが変わらない |


```Gemfile:Gemfile
source "https://rubygems.org"

gem "rails", "~> 7.0.4"

gem "mysql2", ">= 0.5"

```
