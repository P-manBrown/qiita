---
title: 【Rails】タイムゾーンの変更の仕方【初学者の疑問点を簡潔に解説】
tags:
  - Rails
  - タイムゾーン
  - 初学者
private: false
updated_at: '2021-12-25T03:22:54+09:00'
id: 4f93e1d7f441cbfcb5cc
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに
　本記事は、プログラミングの学習を始めて1ヶ月の初学者が、学習を進めていて疑問に思った点について調べた結果を備忘録も兼ねてまとめたものです。
　そのため、記事の内容に誤りが含まれている可能性があります。ご容赦ください。
　間違いを見つけた方は、お手数ですが、ご指摘いただけますと幸いです。

## 今回の疑問点
　今回の疑問点は、

　　_タイムゾーンの変更の仕方について_
　
　です。　


## 疑問点についての解説

###結論

config/application.rbファイルのApplicationクラスに`config.time_zone = 'Tokyo'`を追記することでタイムゾーンを日本標準時間に変更することができます。


###詳しい手順
RailsではデフォルトのタイムゾーンはUTC(協定時)となっています。
created_atメソッドやupdated_atメソッドを使って時間を表示させると`2021-12-25 07:17:23 UTC`のよう9時間前の時刻が表示されると思います。
日本標準時間に設定するためには、config/application.rbファイルのApplicationクラスに以下のとおり
`config.time_zone = 'Tokyo'`を記述します。

``` config/application.rb

module sample_app
  class Application < Rails::Application
    # Initialize configuration defaults for originally generated Rails version.
    config.load_defaults 5.2

    config.i18n.default_locale = :ja
    config.i18n.load_path += Dir[Rails.root.join('config/locales/*.yml').to_s]

    #タイムゾーンの変更
    config.time_zone = 'Tokyo'

    # Settings in config/environments/* take precedence over those specified here.
    # Application configuration can go into files in config/initializers
    # -- all .rb files in that directory are automatically loaded after loading
    # the framework and any gems in your application.
  end

```

記述後にcreated_atメソッドやupdated_atメソッドを使った日時の表示が、`2021-12-25 16:17:23 +0900`となっていれば成功です。


## まとめ
最後にポイントをまとめます。

- タイムゾーンを変更するためには、config/application.rbファイルのApplicationクラスに`config.time_zone = 'Tokyo'`を追記する
