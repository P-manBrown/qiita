---
title: 【Rails】persisted?メソッドの使い方
tags:
  - 'Rails'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## persisted? メソッドとは

`persisted?` メソッドは、レコードが永続化されているかどうかを真偽値で返します。

## create メソッドでの活用例

`create` メソッドはバリデーションエラーが発生しても例外を発生させません。そのため、レコードが正常に保存されたかを確認するには `persisted?` を使用します。

### 成功ケース

```ruby
user = User.create(name: "太郎")
user.persisted?
# => true（レコードが正常に保存された）

user.valid?
# => true

user.errors.empty?
# => true
```

### バリデーションエラーによる失敗ケース

```ruby
# nameカラムにunique制約があると仮定
user = User.create(name: "太郎") # 既存のレコードと重複
user.persisted?
# => false（レコードが保存されなかった）

user.valid?
# => false

user.errors.present?
# => true

user.errors.full_messages
# => ["Name はすでに存在します"]
```



