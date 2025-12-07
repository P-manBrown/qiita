---
title: 【ReactHookForm】isDirtyが誤判定される問題の対処法
tags:
  - ReactHookForm
private: false
updated_at: '2025-12-07T23:56:34+09:00'
id: 069ef35c321a90446b07
organization_url_name: null
slide: false
ignorePublish: false
---
## 問題

React Hook Formで何も入力していないのに`isDirty`が`true`になってしまう場合があります。特に`dirtyFields`は空なのに`isDirty`だけが`true`になっているケースです。

## 対処法

### 1. すべてのフィールドに`defaultValues`を指定する

すべてのフィールドに対して`defaultValues`を明示的に指定します。

```typescript
// NG: 一部のフィールドのみ定義
const form = useForm({
  defaultValues: {
    foo: ""
  }
});

// OK: すべてのフィールドを定義
const form = useForm({
  defaultValues: {
    foo: "",
    bar: undefined // undefinedも明示的に指定
  }
});
```

### 2. dirtyFields`で判定する

動的なフォームなど、全フィールドの`defaultValues`を事前に定義するのが困難な場合は、`dirtyFields`が空かどうかで判定します。

```typescript
const { formState: { dirtyFields } } = useForm();

// dirtyFieldsの長さで判定
const hasDirtyFields = Object.keys(dirtyFields).length > 0;
```

このアプローチにより、実際にフィールドが変更されたかどうかを正確に判定できます。

## 参考

https://www.react-hook-form.com/api/useform/formstate/

https://github.com/react-hook-form/react-hook-form/issues/4740#issuecomment-902545903
