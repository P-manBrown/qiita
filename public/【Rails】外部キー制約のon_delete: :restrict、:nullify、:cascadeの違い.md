---
title: '【Rails】外部キー制約のon_delete: :restrict、:nullify、:cascadeの違い'
tags:
  - 'Rails'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## `on_delete`

Railsでデータベースの外部キー制約を設定する際、`on_delete`で親レコードが削除されたときの動作を制御できます。

## オプション

`on_delete`には`:restrict`、`:nullify`、`:cascade`を指定できます。

### :restrict

**親レコードの削除を阻止**

```ruby
add_foreign_key "revisions", "users", column: "created_by_id", on_delete: :restrict
```

`user`に関連する`revisions`が存在する場合、その`user`の削除はエラーとなります。

### :nullify

**関連する外部キーをnullに設定**

```ruby
add_foreign_key "revisions", "users", column: "created_by_id", on_delete: :nullify
```

`user`が削除されると、関連する`revisions`の`created_by_id`が`null`になる

### :cascade

**関連レコードも連鎖削除**

```ruby
add_foreign_key "revisions", "users", column: "created_by_id", on_delete: :cascade
```

`user`が削除されると、関連する`revisions`も自動的に削除される

## まとめ

| オプション | 動作 |
|-----------|------|
| `:restrict` | 削除を阻止 |
| `:nullify` | 外部キーをnullに |
| `:cascade` | 関連レコードも削除 |
