---
title: 【ReactHookForm】Zodのtransformを使用する方法
tags:
  - ReactHookForm
private: false
updated_at: '2025-12-06T21:59:37+09:00'
id: 5795929c9f2500de19a3
organization_url_name: null
slide: false
ignorePublish: false
---
## 問題点

Zodスキーマで`transform`を使用すると、入力型（`z.input`）と出力型（`z.output`）が異なります。
しかし、`useForm`にジェネリクスを1つだけ指定すると、`handleSubmit`のコールバック関数で受け取るデータの型が正しく推論されません。

```typescript
const fileListSchema = z.custom<FileList>((val) => val instanceof FileList);

const schema = z.object({
  avatar: fileListSchema.transform((fileList) => fileList.item(0)),
});

const { register, handleSubmit } = useForm<z.infer<typeof schema>>({
  resolver: zodResolver(schema),
});

// ❌ avatarの型がFileではなくFileListになってしまう
```

## 解決方法

`useForm`は3つのジェネリック型パラメータを受け取ります。

1. `TFieldValues` - フォームの入力型（変換前の型）
2. `TContext` - コンテキスト型（通常は`object`）
3. `TTransformedValues` - 出力型（変換後の型）

これらを明示的に指定することで、型推論が正しく動作します。

```typescript
const { register, handleSubmit, getValues, formState } = useForm<
  z.input<typeof schema>,   // 入力型（defaultValuesの型）
  unknown,                    // コンテキスト型
  z.output<typeof schema>    // 出力型（handleSubmitで受け取る型）
>({
  resolver: zodResolver(schema),
});

// ✅ avatarの型が正しくFileになる
```

## 例

### FileListをFileに変換

```typescript
import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { z } from 'zod';

const fileListSchema = z.custom<FileList>((val) => val instanceof FileList);

const schema = z.object({
  avatar: fileListSchema.transform((fileList) => fileList.item(0)),
});

export function MyForm() {
  const { register, handleSubmit, formState: { errors } } = useForm<
    z.input<typeof schema>,
    unknown,
    z.output<typeof schema>
  >({
    resolver: zodResolver(schema),
  });

  const onSubmit = (data: z.output<typeof schema>) => {
    // data.avatarの型はFile | null
    console.log(data.avatar);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input type="file" {...register('avatar')} />
      <button type="submit">送信</button>
    </form>
  );
}
```

### 文字列を数値に変換

```typescript
const schema = z.object({
  age: z.string().transform((val) => parseInt(val, 10))
});

const { register, handleSubmit } = useForm<
  z.input<typeof schema>,
  object,
  z.output<typeof schema>
>({
  resolver: zodResolver(schema),
});

const onSubmit = (data: z.output<typeof schema>) => {
  console.log(typeof data.age); // "number"
};
```

## 参考

https://react-hook-form.com/ts#UseFormProps

https://github.com/react-hook-form/resolvers/issues/416#issuecomment-2051680714

https://zod.dev/?id=type-inference
