---
title: 【Rails API】rack-corsでレスポンスヘッダーにアクセスできるようにする方法
tags:
  - Rails
private: false
updated_at: '2024-03-27T00:05:42+09:00'
id: ff0cac3e43f1cb78c10f
organization_url_name: null
slide: false
ignorePublish: false
---
`rack-cors`をインストールして`config/initializers/cors.rb`の`expose`を記述することでJavaScriptからレスポンスヘッダーにアクセスできるようになります。


```rb
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins 'localhost:3000'

    resource "*",
             headers: :any,
             methods: %i[get post put patch delete options head],
             expose: %w[X-Sample],
             credentials: true
  end
end
```

上記の場合には`X-Sample`にアクセス可能になります。

https://github.com/cyu/rack-cors
