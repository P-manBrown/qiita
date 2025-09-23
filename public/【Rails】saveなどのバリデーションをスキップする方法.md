---
title: 【Rails】saveなどのバリデーションをスキップする方法
tags:
  - 'Rails'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## `save(validate: false)`

以下のようにするとバリデーションをスキップできます。

```ruby
user = User.new(name: "", email: "invalid-email")
user.save(validate: false)  # validationをスキップして保存
```

### 使用例

```ruby
# 通常のsave（validationが実行される）
user = User.new(name: "", email: "invalid-email")
user.save  # => false（validationエラーのため保存されない）

# validationをスキップしたsave
user = User.new(name: "", email: "invalid-email")
user.save(validate: false)  # => true（validationをスキップして保存される）
```
