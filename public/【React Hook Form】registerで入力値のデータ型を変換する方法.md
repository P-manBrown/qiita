---
title: 【ReactHookForm】registerで入力値のデータ型を変換する方法
tags:
  - ReactHookForm
private: false
updated_at: '2025-12-04T00:01:04+09:00'
id: ab693b3c45019e85b951
organization_url_name: null
slide: false
ignorePublish: false
---
## データ型変換オプション

### valueAsNumber

入力値を数値型に変換します。変換に失敗した場合は`NaN`が返されます。

- バリデーションの前に変換処理が実行される
- `number`型のinputにのみ適用
- `defaultValue`や`defaultValues`には影響しない

```jsx
<input
  type="number"
  {...register("age", { valueAsNumber: true })}
/>
```

### valueAsDate

入力値を`Date`型に変換します。変換に失敗した場合は`Invalid Date`が返されます。

- バリデーションの前に変換処理が実行される
- `defaultValue`や`defaultValues`には影響しない

```jsx
<input
  type="date"
  {...register("birthday", { valueAsDate: true })}
/>
```

### setValueAs

カスタム変換関数を定義できます。任意の変換ロジックを実装可能です。

- バリデーションの前に変換処理が実行される
- `valueAsNumber`や`valueAsDate`が`true`の場合は無視される
- テキスト入力にのみ適用
- `defaultValue`や`defaultValues`には影響しない

```jsx
<input
  {...register("price", {
    setValueAs: (value) => parseFloat(value) || 0
  })}
/>
```

## 参考

https://react-hook-form.com/docs/useform/register
