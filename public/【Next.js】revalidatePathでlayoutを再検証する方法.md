---
title: 【Next.js】revalidatePathでlayoutを再検証する方法
tags:
  - 'Next.js'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## revalidatePathの基本構文

```typescript
revalidatePath(path: string, type?: 'page' | 'layout'): void
```

`revalidatePath`関数は2つのパラメータを受け取ります：

- `path`: 再検証したいパスの文字列（1024文字未満、大文字小文字を区別）
- `type`: 再検証するパスのタイプを指定する（オプション）

## layoutを再検証する方法

`type`に`'layout'`を指定するとレイアウトファイルにマッチするURLと、そのレイアウトを使用するすべての下位ページを再検証します。

```typescript
import { revalidatePath } from 'next/cache'

export async function revalidateBlogLayout() {
  // /blog/[slug] レイアウトとそれを使用する下位ページをすべて再検証
  revalidatePath('/blog/[slug]', 'layout')
  
  // ルートグループを使用している場合
  revalidatePath('/(main)/post/[slug]', 'layout')
}
```
