---
title: 【DeviseTokenAuth】paranoidモードを有効化する方法
tags:
  - devise_token_auth
private: false
updated_at: '2025-06-05T23:42:29+09:00'
id: 526895a852aa364b68f9
organization_url_name: null
slide: false
ignorePublish: false
---

## paranoidモードとは

有効化するとパスワードリセットなどのために提供されたがメールアドレスか正しいか間違っているかに関わらず、同じ動作をするようになります。
これにより、特定のメールアドレスが登録されていないことを第三者に知られることを防止できます。

## 有効化する方法

`config/initializers/devise.rb`に以下のように記述することで有効化できます。

```ruby
Devise.setup do |config|
  config.paranoid = true
end
```

