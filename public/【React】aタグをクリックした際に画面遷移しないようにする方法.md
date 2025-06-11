---
title: 【React】aタグをクリックした際に画面遷移しないようにする方法
tags:
  - 'React'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

## `event.preventDefault()` を使用する

`onClick`ハンドラに渡されるイベントオブジェクトで `preventDefault()` を呼び出すと画面遷移しないようにできます。

```jsx
function NoNavLink() {
  const handleClick = (event) => {
    // 画面遷移を無効化
    event.preventDefault()
    console.log('画面遷移をキャンセル')
    // 任意の処理
  }

  return (
    <a href="https://example.com" onClick={handleClick}>
      画面遷移をしないリンク
    </a>
  )
}

export default NoNavLink
```

## `javascript:void(0)` を使用する

`href`属性に `javascript:void(0)` を指定すると、ブラウザが「何も起こさないURL」として扱うため、画面遷移を発生させません。

```jsx
function VoidLink() {
  const handleClick = () => {
    console.log('javascript:void(0)で遷移しない')
    // 任意の処理
  }

  return (
    <a href="javascript:void(0)" onClick={handleClick}>
      遷移しないリンク (void)
    </a>
  )
}

export default VoidLink
```
