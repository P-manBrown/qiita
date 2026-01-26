---
title: 【Zed】未使用コードの明度を設定する方法
tags:
  - 'ZedEditor'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定値を追加

`settings.json`に以下の設定を追加します。 
```json
{
  "unnecessary_code_fade": 0.5
}
```

## 設定値の範囲

- **デフォルト値**: `0.3`
- **設定可能範囲**: `0.0`〜`0.9`
- `0.0`: フェードアウトなし（未使用コードも通常通り表示）
- `0.9`: 最大限フェードアウト（未使用コードが非常に薄く表示） 

## 参考

https://zed.dev/docs/configuring-zed#unnecessary-code-fade
