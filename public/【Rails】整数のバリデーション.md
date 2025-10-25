---
title: 【Rails】整数のバリデーション
tags:
  - Rails
private: false
updated_at: '2025-10-25T23:43:48+09:00'
id: 64498748d01c60475f38
organization_url_name: null
slide: false
ignorePublish: false
---
## 0以上の整数のみを許可

```ruby
class Product < ApplicationRecord
  validates :stock, numericality: { greater_than_or_equal_to: 0, only_integer: true }
end
```

- `greater_than_or_equal_to: 0` で0以上を指定
- `only_integer: true` で整数のみを許可

## 1以上の整数のみを許可

```ruby
class Order < ApplicationRecord
  validates :quantity, numericality: { greater_than: 0, only_integer: true }
end
```

## まとめ

| 条件                | バリデーション                                               |
| ------------------- | ------------------------------------------------------------ |
| 0以上の整数         | `numericality: { greater_than_or_equal_to: 0, only_integer: true }` |
| 1以上の整数 | `numericality: { greater_than: 0, only_integer: true }`      |

