---
title: ' 【Ruby】文字列を数値に変換する方法'
tags:
  - Ruby
private: false
updated_at: '2024-12-02T23:58:50+09:00'
id: 5af28a08ebea8ad7a9cf
organization_url_name: null
slide: false
ignorePublish: false
---
文字列を数値に変換するには`.to_i`メソッドを使用します。

```ruby
value = "123"
integer_value = value.to_i
puts integer_value  
# 123
```

文字列が整数に変換可能な場合にはその整数値が返されます。
変換できない場合には、`0`が返されます。

```ruby
value = "abc"
integer_value = value.to_i
puts integer_value  
# 0
```
