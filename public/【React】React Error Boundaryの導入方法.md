---
title: 【React】React Error Boundaryの導入方法
tags:
  - 'React'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
React Error Boundaryは、Reactアプリケーションでエラーハンドリングを簡単に実装できるライブラリです。エラーが発生した際にフォールバックUIを表示し、アプリ全体のクラッシュを防ぐことができます。

## インストール

```sh
npm install react-error-boundary
```

## 基本的な使い方

### 1. シンプルなエラー表示

最もシンプルな方法は`fallback`プロパティを使用する方法です。

```jsx
"use client";
import { ErrorBoundary } from "react-error-boundary";

<ErrorBoundary fallback={<div>エラーが発生しました</div>}>
  <YourApp />
</ErrorBoundary>
```

### 2. カスタムフォールバックコンポーネント

エラー情報を表示したり、リトライボタンを追加する場合は`FallbackComponent`を使用します。

```jsx
function ErrorFallback({ error, resetErrorBoundary }) {
  return (
    <div role="alert">
      <p>エラーが発生しました:</p>
      <pre style={{ color: "red" }}>{error.message}</pre>
      <button onClick={resetErrorBoundary}>再試行</button>
    </div>
  );
}

<ErrorBoundary FallbackComponent={ErrorFallback}>
  <YourApp />
</ErrorBoundary>
```

### 3. エラーログの記録

`onError`を使用してエラーを外部サービスに送信できます。

```jsx
const logError = (error, info) => {
  console.error("エラー:", error);
  // 外部APIにログを送信
};

<ErrorBoundary FallbackComponent={ErrorFallback} onError={logError}>
  <YourApp />
</ErrorBoundary>
```

## useErrorBoundaryフック

非同期処理やイベントハンドラー内のエラーを捕捉する場合は`useErrorBoundary`フックを使用します。

```jsx
import { useErrorBoundary } from "react-error-boundary";

function MyComponent() {
  const { showBoundary } = useErrorBoundary();

  const handleClick = async () => {
    try {
      await fetchData();
    } catch (error) {
      showBoundary(error);
    }
  };

  return <button onClick={handleClick}>データ取得</button>;
}
```
