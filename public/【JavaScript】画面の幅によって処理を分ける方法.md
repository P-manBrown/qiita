---
title: 【JavaScript】画面の幅によって処理を分ける方法
tags:
  - 'javascript'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

## 画面の幅を検証する方法

画面の幅が一定の値か検証するには`window.matchMedia()`を使用します。

```javascript
// ウィンドウサイズが640px以下ならtrue
matchMedia('(min-width:640px)').matches

// ウィンドウサイズが768px以上1024px以下ならtrue
matchMedia('(min-width:768px) and (max-width:1024px)').matches
```

## 画面幅が変更された際に処理を分ける

画面幅が変更された際に画面の幅を検証し、処理を分けるには以下のようにします。

```javascript
const mediaQueryList = matchMedia('(min-width:640px)')

mediaQueryList.addEventListener('change', (ev) => {
    if (ev.matches) {
        console.log('画面幅：640px以上')
    } else {
        console.log('画面幅：640px未満')
    }
})
```

## 参考

https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia
