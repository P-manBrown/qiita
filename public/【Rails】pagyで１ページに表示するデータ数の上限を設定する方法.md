---
title: 【Rails】pagyで１ページに表示するデータ数の上限を設定する方法
tags:
  - 'Rails'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## limitの設定方法

`limit`の値を変更することで１ページに表示するデータの最大数を設定できます。

### グローバルなデフォルト設定

アプリケーション全体で使用するデフォルトの`limit`を設定できます。

```ruby
# config/initializers/pagy.rb
Pagy::DEFAULT[:limit] = 25
```

この設定により、すべてのPagyインスタンスで1ページあたり25件のアイテムが表示されます。

### 個別インスタンスでのlimit指定

特定のページネーションインスタンスでのみ`limit`を変更したい場合：

```ruby
# app/controllers/products_controller.rb
class ProductsController < ApplicationController
  def index
    @pagy, @products = pagy(Product.all, limit: 30)
  end
end
```

この例では、デフォルト設定を無視して1ページあたり30件の商品を表示します。

###  ActiveRecordのlimitとの関係

Pagyの`limit`オプションは、ActiveRecordで既に設定されている`limit`を上書きします：

```ruby
# Productモデルで既にlimit(5)が設定されていても、
# Pagyのlimit: 10が優先される
@pagy, @products = pagy(Product.limit(5), limit: 10)
# 実際のクエリでは limit 10 が使用される
```

## limit関連のオプション

### 最大limit値の制限

セキュリティ上の理由から、ユーザーが指定できる最大limit値を制限できます：

```ruby
# config/initializers/pagy.rb
require 'pagy/extras/limit'

Pagy::DEFAULT[:limit_max] = 100  # 最大100件まで
```

###  limitパラメータ名のカスタマイズ

URLパラメータの名前を変更できます：

```ruby
# config/initializers/pagy.rb
Pagy::DEFAULT[:limit_param] = :per_page  # ?per_page=25
```

### limit extraの無効化

特定のインスタンスでlimit extraを無効にする：

```ruby
@pagy, @records = pagy(collection, limit_extra: false)
```

