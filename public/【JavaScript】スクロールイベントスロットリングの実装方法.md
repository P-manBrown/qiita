---
title: 【JavaScript】スクロールイベントスロットリングの実装方法
tags:
  - JavaScript
private: false
updated_at: '2025-11-09T23:53:56+09:00'
id: f1913f0a145a196b6fb4
organization_url_name: null
slide: false
ignorePublish: false
---
## 実装例

以下は、スクロール位置を20ミリ秒ごとにスロットリングして処理する例です。

```javascript
let lastKnownScrollPosition = 0;
let ticking = false;

function doSomething(scrollPos) {
  // スクロール位置を使った処理をここに記述
  console.log('スクロール位置:', scrollPos);
}

document.addEventListener("scroll", (event) => {
  lastKnownScrollPosition = window.scrollY;
  
  if (!ticking) {
    // 20ミリ秒ごとに処理を実行するようスロットリング
    setTimeout(() => {
      doSomething(lastKnownScrollPosition);
      ticking = false;
    }, 20);
    
    ticking = true;
  }
});
```

1. **tickingフラグ**: 処理が実行中かどうかを管理
2. **lastKnownScrollPosition**: 最新のスクロール位置を保持
3. **setTimeout**: 指定した間隔（この例では20ms）で処理を実行

### 動作の流れ

1. スクロールイベントが発火
2. 最新のスクロール位置を記録
3. `ticking` が `false` の場合のみ、タイマーをセット
4. タイマーが満了したら処理を実行し、`ticking` を `false` に戻す
5. その間に発火したスクロールイベントは無視され、最新の位置だけが保持される

## IntersectionObserver

要素の可視性を監視するだけであれば、スクロールイベントではなく`IntersectionObserver` の使用を使用して以下のように実装できます。

```javascript
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      // 要素が表示されたときの処理
    }
  });
});

observer.observe(document.querySelector('.target-element'));
```

## requestAnimationFrameは使わない

`requestAnimationFrame()` を使ってスクロールイベントをスロットリングするのは、アニメーションフレームコールバックとスクロールイベントハンドラは同じ頻度で発火するため、**効果がありません**。

代わりに `setTimeout()` を使って自分でタイムアウトを管理する必要があります。

## 参考

https://developer.mozilla.org/en-US/docs/Web/API/Document/scroll_event#scroll_event_throttling
