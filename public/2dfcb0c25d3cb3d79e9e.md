---
title: 【Rails】ActiveStorageにバリデーションを設定する方法
tags:
  - Rails
  - ActiveStorage
private: false
updated_at: '2024-04-22T05:54:57+09:00'
id: 2dfcb0c25d3cb3d79e9e
organization_url_name: null
slide: false
ignorePublish: false
---
## Gemをインストールする

`active_storage_validations`をインストールします。

https://github.com/igorkasyanchuk/active_storage_validations

```rb:Gemfile
gem 'active_storage_validations'

# :dimension　または　:aspect_ratioを使用する場合には以下のいずれかを併せてインストールします。
gem 'mini_magick', '>= 4.9.5'
gem 'ruby-vips', '>= 2.1.0'

```

```terminal:ターミナル
bundle install 
```

## バリデーションを設定する

モデルにバリデーションを記述します。

```app/models/user.rb
class User < ApplicationRecord
  has_one_attached :avatar

  validates :avatar, content_type: { in: %w[image/jpeg image/png] }, size: { less_than_or_equal_to: 2.megabytes }
end
```

上記の場合にはjpegおよびpngのファイルで2MB以下のものを許可します。
