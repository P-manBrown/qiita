---
title: 【Next.js】Linkでクエリパラメータを変更した際にSuspenseによるローディングUIを表示する方法
tags:
  - Next.js
private: false
updated_at: '2025-07-31T23:45:48+09:00'
id: 08198131dd6290fede6a
organization_url_name: null
slide: false
ignorePublish: false
---
## 問題

Next.jsのApp Routerで`Link`コンポーネントを使用して同じパスのクエリーパラメーターのみを変更した場合、`Suspense`の`fallback`が表示されません。

```tsx
<Link href={{ query: { name: 'test' }}}>
  Sample
</Link>
```

## 解決策

`Suspense`の`key`にクエリパラメータを渡すことで`fallback`が表示されるようになります。

```tsx:page.tsx
import { Suspense } from "react";
import { DataComponent } from "./DataComponent";
import { LoadingSkeleton } from "./LoadingSkeleton";

export default function Page({ 
  searchParams 
}: { 
  searchParams: Promise<{ [key: string]: string | string[] | undefined }> 
}) {
  const filters = (await searchParams).filters;
  
  return (
    <div>
      <SearchInput />
      
      {/* keyプロパティを追加してSuspense境界をリセット */}
      <Suspense 
        key={filters}
        fallback={<LoadingSkeleton />}
      >
        <DataComponent filters={filters} />
      </Suspense>
    </div>
  );
}
```

## 参考

https://github.com/vercel/next.js/issues/53543

https://react.dev/reference/react/Suspense#resetting-suspense-boundaries-on-navigation
