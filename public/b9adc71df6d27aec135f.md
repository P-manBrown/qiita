---
title: 【Next.js】conformの導入方法
tags:
  - Next.js
private: false
updated_at: '2024-09-09T00:00:29+09:00'
id: b9adc71df6d27aec135f
organization_url_name: null
slide: false
ignorePublish: false
---
## インストール

以下のコマンドを実行して必要なライブラリをインストールします。

```terminal
yarn add @conform-to/react @conform-to/zod
```

## Zodのスキーマを作成する

バリデーションのため、Zodのスキーマを作成します。

```ts:schema.ts
import { z } from "zod";

export const loginSchema = z.object({
  email: z.string().email(),
  password: z.string(),
});

```

## サーバーアクションを作成

```ts:action.ts
"use server";

import { redirect } from "next/navigation";
import { parseWithZod } from "@conform-to/zod";
import { loginSchema } from "@/app/schema";

export async function login(prevState: unknown, formData: FormData) {
  const submission = parseWithZod(formData, {
    schema: loginSchema,
  });

  if (submission.status !== "success") {
    return submission.reply();
  }

  redirect("/dashboard");
}
```

## フォームの作成

```tsx:form.tsx
"use client";

import { useForm } from "@conform-to/react";
import { parseWithZod } from "@conform-to/zod";
import { useFormState } from "react-dom";
import { login } from "@/app/actions";
import { loginSchema } from "@/app/schema";

export function LoginForm() {
  const [lastResult, action] = useFormState(login, undefined);
  const [form, fields] = useForm({
    lastResult,
    onValidate({ formData }) {
      return parseWithZod(formData, { schema: loginSchema });
    },
    shouldValidate: "onBlur",
  });

  return (
    <form id={form.id} onSubmit={form.onSubmit} action={action} noValidate>
      <div>
        <label htmlFor={fields.email.id}>>Email</label>
        <input type="email" name={fields.email.name} />
        <div>{fields.email.errors}</div>
      </div>
      <div>
        <label htmlFor={fields.password.id}>Password</label>
        <input type="password" name={fields.password.name} />
        <div>{fields.password.errors}</div>
      </div>
      <label>
        <div>
          <span>Remember me</span>
          <input type="checkbox" name={fields.remember.name} />
        </div>
      </label>
      <Button>Login</Button>
    </form>
  );
}
```
