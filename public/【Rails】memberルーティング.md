---
title: 【Rails】memberルーティング
tags:
  - Rails
private: false
updated_at: '2026-02-22T19:11:00+09:00'
id: 8a63f9d31aedce4a4801
organization_url_name: null
slide: false
ignorePublish: false
---
## 概要

`member`はRailsのルーティングで、**特定のリソースに対するカスタムアクション**を追加する際に使います。
生成されるURLに`:id`が含まれるのが特徴です。

## 基本的な使い方
```ruby
resources :photos do
  member do
    get 'preview'
  end
end
```

上記で以下のルーティングが生成されます。

| HTTPメソッド | URL | コントローラ#アクション |
|---|---|---|
| GET | /photos/:id/preview | photos#preview |

`params[:id]`でリソースのIDを取得でき、`preview_photo_url`・`preview_photo_path`ヘルパーも自動生成されます。

## 別の書き方

ルーティングが1つだけの場合は`on: :member`オプションで簡潔に書けます。
```ruby
resources :photos do
  get 'preview', on: :member
end
```

## :onオプションを省略した場合
```ruby
resources :photos do
  get 'preview'
end
```

同様のルーティングが生成されますが、以下の点が変わります。

- IDの取得：`params[:id]` → `params[:photo_id]`
- ヘルパー名：`preview_photo_url` → `photo_preview_url`

## 使用できるHTTPメソッド

`get`の他に`post`、`patch`、`put`、`delete`も使用できます。

## 参考

https://railsguides.jp/routing.html#%E3%83%A1%E3%83%B3%E3%83%90%E3%83%BC%E3%83%AB%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0%E3%82%92%E8%BF%BD%E5%8A%A0%E3%81%99%E3%82%8B
