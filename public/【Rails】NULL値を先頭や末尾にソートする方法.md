---
title: 【Rails】NULL値を先頭や末尾にソートする方法
tags:
  - Rails
private: false
updated_at: '2025-10-26T21:30:02+09:00'
id: 18082f499968c0d823da
organization_url_name: null
slide: false
ignorePublish: false
---
## NULLを先頭にする

```ruby
Procedure.order(Procedure.arel_table[:name].desc.nulls_first)
# => SELECT "procedures".* FROM "procedures" ORDER BY "procedures"."name" DESC NULLS FIRST
```

## NULLを末尾にする

```ruby
Procedure.order(Procedure.arel_table[:name].asc.nulls_last)
# => SELECT "procedures".* FROM "procedures" ORDER BY "procedures"."name" ASC NULLS LAST
```

## 参考

https://github.com/rails/rails/pull/38131

https://github.com/rails/rails/pull/42245
