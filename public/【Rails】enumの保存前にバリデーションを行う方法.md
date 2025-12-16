---
title: 【Rails】enumの保存前にバリデーションを行う方法
tags:
  - Rails
private: false
updated_at: '2025-12-16T22:49:13+09:00'
id: 8e875a880962533bc735
organization_url_name: null
slide: false
ignorePublish: false
---
## enumの基本的な定義
```ruby
class Conversation < ApplicationRecord
  enum :status, [:active, :archived]
end
```

## デフォルトの挙動：ArgumentErrorが発生

デフォルトでは、無効な値を代入すると`ArgumentError`が即座に発生します。

```ruby
class Conversation < ApplicationRecord
  enum :status, [:active, :archived]
end
```

```ruby
conversation = Conversation.new
conversation.status = :unknown  # => ArgumentError: 'unknown' is not a valid status
```

## validateオプションの使用

`validate: true`を指定すると、代入時にエラーを発生させず、`valid?`メソッドでバリデーションを行えます。

```ruby
class Conversation < ApplicationRecord
  enum :status, [:active, :archived], validate: true
end
```

```ruby
conversation = Conversation.new

conversation.status = :unknown
conversation.valid?  # => false

conversation.status = nil
conversation.valid?  # => false

conversation.status = :active
conversation.valid?  # => true
```

## nil値を許可する

`validate`オプションにハッシュを渡すことで、追加のバリデーションオプションを指定できます。
```ruby
class Conversation < ApplicationRecord
  enum :status, [:active, :archived], validate: { allow_nil: true }
end
```

```ruby
conversation = Conversation.new

conversation.status = :unknown
conversation.valid?  # => false

conversation.status = nil
conversation.valid?  # => true

conversation.status = :active
conversation.valid?  # => true
```

## 参考

https://edgeapi.rubyonrails.org/classes/ActiveRecord/Enum.html
