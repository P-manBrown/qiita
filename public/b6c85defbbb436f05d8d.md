---
title: 【DeviseTokenAuth】UnsafeRedirectError解消法
tags:
  - Rails
  - devise_token_auth
private: false
updated_at: '2024-01-26T06:44:44+09:00'
id: b6c85defbbb436f05d8d
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

DeviseTokenAuthを使用している際に`redirect_to`が実行されると`UnsafeRedirectError`が発生します。

エラーに関する詳細は以下のページをご参照ください。

https://api.rubyonrails.org/v7.1/classes/ActionController/Redirecting.html#method-i-redirect_to

## 解消法

外部リダイレクトしているコントローラーに以下を追加します。

```rb
  def redirect_options
    { allow_other_host: true }
  end
```

## 参考

https://github.com/lynndylanhurley/devise_token_auth/pull/1599

https://github.com/lynndylanhurley/devise_token_auth/issues/1536
