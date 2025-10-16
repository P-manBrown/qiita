---
title: 【Rails】saveなどのバリデーションをスキップする方法
tags:
  - Rails
private: false
updated_at: '2025-09-23T23:58:40+09:00'
id: be4c3938e1a0e4630f9e
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
