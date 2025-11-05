---
title: 【JavaScript】 Intersection Observer APIの使い方
tags:
  - JavaScript
private: false
updated_at: '2025-11-04T23:48:23+09:00'
id: 55f14b0f1b0a0379d6d8
organization_url_name: null
slide: false
ignorePublish: false
---
## Intersection Observer APIとは

Intersection Observer APIは、要素がビューポート（または指定した親要素）と交差する変化を非同期的に監視するためのAPIです。

## 主な用途

- 画像の遅延読み込み（Lazy Loading）
- 無限スクロールの実装
- 広告の可視性測定
- 要素の可視状態に応じたアニメーション制御

## 基本的な使い方

### 1. オブザーバーの作成

```javascript
// コールバック関数の定義
const callback = (entries, observer) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      console.log('要素が表示されました');
      // 処理を実行
    }
  });
};

// オプションの設定
const options = {
  root: null,           // ビューポートを基準にする
  rootMargin: '0px',    // マージン（CSSのmarginと同様）
  threshold: 0.5        // 50%表示されたら発火
};

// オブザーバーの生成
const observer = new IntersectionObserver(callback, options);
```

### 2. 監視対象の要素を登録

```javascript
const targetElement = document.querySelector('#target');
observer.observe(targetElement);
```

## オプションの詳細

### root
監視の基準となる要素。`null`の場合はビューポートが使用されます。

```javascript
root: document.querySelector('#scrollArea')
```

### rootMargin
ルート要素の周囲のマージン。CSSのmarginプロパティと同じ形式で指定します。

```javascript
rootMargin: '10px 20px 30px 40px'  // 上 右 下 左
```

### threshold
コールバックを実行する交差率の閾値。0.0〜1.0の数値または配列で指定します。

```javascript
threshold: 0.5              // 50%表示されたとき
threshold: [0, 0.25, 0.5, 0.75, 1.0]  // 25%ごと
```

## コールバック関数で取得できる情報

```javascript
const callback = (entries) => {
  entries.forEach(entry => {
    console.log(entry.isIntersecting);      // 交差しているか
    console.log(entry.intersectionRatio);   // 交差率（0.0〜1.0）
    console.log(entry.target);              // 監視対象の要素
    console.log(entry.boundingClientRect);  // 要素の位置情報
    console.log(entry.rootBounds);          // ルート要素の位置情報
    console.log(entry.intersectionRect);    // 交差領域の情報
  });
};
```

## 監視の解除

```javascript
// 特定の要素の監視を解除
observer.unobserve(targetElement);

// すべての監視を解除
observer.disconnect();
```

## 参考

https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API
