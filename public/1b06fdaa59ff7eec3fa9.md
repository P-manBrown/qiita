---
title: 【React】React Hooksについて
tags:
  - hooks
  - React
  - 初学者
private: false
updated_at: '2022-01-02T00:27:04+09:00'
id: 1b06fdaa59ff7eec3fa9
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに
　本記事は、プログラミングの学習を始めて1ヶ月の初学者が、学習を進めていて疑問に思った点について調べた結果を備忘録も兼ねてまとめたものです。
　そのため、記事の内容に誤りが含まれている可能性があります。ご容赦ください。
　間違いを見つけた方は、お手数ですが、ご指摘いただけますと幸いです。

##React 入門

###React Hooksとは
以前はクラスコンポーネントでしか使えなかったstateやライフサイクルを関数コンポーネントでも使える機能です。
フックを使うことでよりシンプルに記述をすることができるようになりました。

主なフックは以下の通りです。

`useState()`
`useEffect()`

### useStateの使い方
関数コンポーネントでローカルstateを使用することができます。

```Sample.js
// useStateをインポート
import React, { useState } from 'react';

// 宣言
const [state変数名, state更新関数名] = useState(state初期値)

// stateの呼び出し
{ state変数名 }

```

### useEffectの使い方
ライフサイクルメソッドの代替として、関数コンポーネントで利用できます。
具体的には、以下のメソッドの代替として使用できます。
`componentDidMout()`
`componentDidUpdate()`
`componentWillUnmount()`

```Sample.js
// レンダー毎に実行する場合
useEffect(() => {
  // コンポーネントがレンダーされる時（再レンダー含む）に実行
  return () => {
    // コンポーネントが破棄される時に実行
  }
})

// マウント時のみ実行する場合
useEffect(() => {
  // コンポーネントがレンダーされる時に実行
}, [])

// 特定のstateやpropsが更新された時に実行する場合
useEffect(() => {
  // コンポーネントがレンダーされる時に実行される。
  return () => {
    // コンポーネントが破棄される時に実行される。
  }
}, [変更されるstateやprops])


// マウント時とアンマウント時のみ実行する場合
useEffect(() => {
  // コンポーネントがレンダーされる時に実行される。
  return () => {
    // コンポーネントが破棄される時に実行される。
  }
}, [])


```


## まとめ

- hookはstateやライフサイクルを関数コンポーネントでも使えるようになる機能
- useState()はstateの代替
- useEffect()はライフサイクルメソッドの代替

