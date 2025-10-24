---
title: 【Rails】日付比較バリデーション
tags:
  - 'Rails'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## Rails 7以降の方法

`ComparisonValidator`を使用します。

```ruby
class Event < ApplicationRecord
  validates :start_date, presence: true
  validates :end_date, presence: true
  validates :end_date, comparison: { greater_than: :start_date }
  
  # または
  validates_comparison_of :end_date, greater_than: :start_date
end
```

### 利用可能な比較オプション

- `greater_than`: より大きい
- `greater_than_or_equal_to`: 以上
- `equal_to`: 等しい
- `less_than`: より小さい
- `less_than_or_equal_to`: 以下
- `other_than`: 等しくない

### 複数の比較条件の組み合わせ

複数の比較オプションを同時に使用できます。

```ruby
class Event < ApplicationRecord
  validates_comparison_of :end_date, 
                          greater_than: :start_date, 
                          other_than: Date.today
end
```

## Rails 7以前の方法

```ruby
class Event < ApplicationRecord
  validates :start_date, presence: true
  validates :end_date, presence: true
  validate :end_date_is_after_start_date

  private

  def end_date_is_after_start_date
    if end_date < start_date
      errors.add(:end_date, 'cannot be before the start date')
    end
  end
end
```

## 参考

https://guides.rubyonrails.org/active_record_validations.html#comparison
