---
title: '【Rails】Faker::Booleanでtrueの比率を指定する方法'
tags:
  - Rails
private: false
updated_at: '2025-09-19T23:31:11+09:00'
id: 14ca810c09dd99002a0e
organization_url_name: null
slide: false
ignorePublish: false
---
## 通常の生成

```ruby
Faker::Boolean.boolean
#=> true または false
```

## 比率を指定した生成

`true_ratio`パラメータを使用してtrueの出現比率を指定できます。

```ruby
# 70% trueを返す
Faker::Boolean.boolean(true_ratio: 0.7)

# 30% trueを返す
Faker::Boolean.boolean(true_ratio: 0.3)

# 90% trueを返す
Faker::Boolean.boolean(true_ratio: 0.9)
```

## 参考

https://github.com/faker-ruby/faker/blob/8fbda8de78d6827cae94bc2dee7dfa4d9a91f261/doc/default/boolean.md
