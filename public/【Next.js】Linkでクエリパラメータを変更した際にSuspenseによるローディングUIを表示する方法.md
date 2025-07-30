---
title: 【Next.js】Linkでクエリパラメータを変更した際にSuspenseによるローディングUIを表示する方法
tags:
  - 'Next.js'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 問題

Next.jsのApp Routerで`Link`コンポーネントを使用して同じパスのクエリーパラメーターのみを変更した場合、`Suspense`のfallbackや`loading.tsx`が表示されない問題があります。

```tsx
// このような遷移でローディングUIが表示されない
<Link href="/search?q=react">React</Link>
<Link href="/search?q=nextjs">Next.js</Link>
```

## 原因

ReactのSuspenseコンポーネントは、同じキーを持つ場合にSuspense境界をリセットしません。Next.jsはクエリーパラメーターをSuspenseのキーに含めていないため、同じルートへの遷移時にローディング状態が表示されません。

参考: [React Suspense ドキュメント](https://react.dev/reference/react/Suspense#resetting-suspense-boundaries-on-navigation)

## 解決策: Suspenseにkeyを追加

### 基本的な実装

```tsx
// page.tsx
import { Suspense } from "react";
import { DataComponent } from "./DataComponent";
import { LoadingSkeleton } from "./LoadingSkeleton";

export default function Page({ 
  searchParams 
}: { 
  searchParams?: Record<string, string | undefined> 
}) {
  // searchParamsからキーを生成
  const suspenseKey = `search=${searchParams?.search || ''}`;
  
  return (
    <div>
      <SearchInput />
      
      {/* keyプロパティを追加してSuspense境界をリセット */}
      <Suspense 
        key={suspenseKey}
        fallback={<LoadingSkeleton />}
      >
        <DataComponent searchParams={searchParams} />
      </Suspense>
    </div>
  );
}
```

### 複数パラメーターの場合

```tsx
export default function Page({ searchParams }) {
  // 複数のパラメーターを組み合わせてキーを作成
  const suspenseKey = [
    searchParams?.search,
    searchParams?.category,
    searchParams?.page
  ].filter(Boolean).join('-');

  return (
    <Suspense 
      key={suspenseKey}
      fallback={<LoadingSkeleton />}
    >
      <ProductList searchParams={searchParams} />
    </Suspense>
  );
}
```

## 参考リンク

- [GitHub Issue #53543](https://github.com/vercel/next.js/issues/53543)
- [React Suspense Documentation](https://react.dev/reference/react/Suspense)
