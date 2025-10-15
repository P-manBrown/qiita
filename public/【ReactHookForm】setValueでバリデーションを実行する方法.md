---
title: 【ReactHookForm】setValueでバリデーションを実行する方法
tags:
  - 'ReactHookForm'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 基本的な使い方

`setValue`の第３引数に`{ shouldValidate: true }`を指定すると、値の設定時にバリデーションが実行されます。

```typescript
import { useForm } from 'react-hook-form';

function MyForm() {
  const { register, setValue, formState: { errors } } = useForm();

  const updateUsername = () => {
    setValue('username', 'newValue', { 
      shouldValidate: true // バリデーションを実行
    });
  };

  return (
    <div>
      <input {...register('username', { 
        required: '必須項目です',
        minLength: { value: 3, message: '3文字以上入力してください' }
      })} />
      {errors.username && <p>{errors.username.message}</p>}
      <button onClick={updateUsername}>値を更新</button>
    </div>
  );
}
```

## 参考

https://www.react-hook-form.com/api/useform/setvalue/
