---
title: 【ReactHookForm】getFieldStateの使い方
tags:
  - 'ReactHookForm'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## getFieldStateとは

`getFieldState`は、React Hook Form v7.25.0で導入されたメソッドで、個別のフィールドの状態を取得できます。型安全な方法でネストされたフィールドの状態を取得したい場合に便利です。

## 基本的な使い方

```tsx
import { useForm } from "react-hook-form";

function App() {
  const {
    register,
    getFieldState,
    formState: { isDirty, isValid },
  } = useForm({
    mode: "onChange",
    defaultValues: {
      firstName: "",
    },
  });

  const fieldState = getFieldState("firstName");

  return (
    <form>
      <input {...register("firstName", { required: true })} />
      <p>{getFieldState("firstName").isDirty && "編集済み"}</p>
      <p>{getFieldState("firstName").isTouched && "タッチ済み"}</p>
      <button
        type="button"
        onClick={() => console.log(getFieldState("firstName"))}
      >
        フィールド状態を表示
      </button>
    </form>
  );
}
```

## 取得できる状態

`getFieldState`で取得できる主な状態は以下のとおりです。

- `isDirty`: フィールドが変更されたかどうか
- `isTouched`: フィールドがタッチ（フォーカス後にブラー）されたかどうか
- `invalid`: フィールドのバリデーションが失敗しているかどうか
- `error`: フィールドのエラー情報

## 注意点

- フィールド名は、登録されたフィールド名と一致する必要があります
  - 存在しないフィールド名を指定すると、状態は`false`、エラーは`undefined`を返します


## 参考

https://react-hook-form.com/docs/useform/getfieldstate
