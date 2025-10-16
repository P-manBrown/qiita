---
title: 【CSS】子要素の状態に応じてスタイルを適用する方法
tags:
  - CSS
private: false
updated_at: '2025-07-26T23:54:35+09:00'
id: 9d31ca0afa5153d75614
organization_url_name: null
slide: false
ignorePublish: false
---
`:has()` を使うと、親要素が持つ子要素の状態（ホバー・フォーカスなど）に応じて親要素自体のスタイルを動的に制御できます。  

## 子要素にフォーカスしている場合に親要素にスタイルを適用する

子の `<button>` にフォーカスが当たっているときのみ、親の `div` に背景色を付与する例です。

```html:html
<div class="focus-container">
  <button>クリックしてフォーカス</button>
</div>
```

```css:css
/* デフォルトのスタイル */
.focus-container {
  background: white;
  padding: 40px;
  text-align: center;
}

/* 子要素 button にフォーカスがあるときは白背景 */
.focus-container:has(button:focus) {
  background: #0000ff;
}
```

## 子要素にホバーしたときに親要素にスタイルを適用する

次に、子要素（例：`<button>`）にマウスオーバー（ホバー）している間、親要素 `div` の背景を青に変える例です。


```html:html
<div class="hover-container">
  <button>マウスオーバー</button>
</div>
```

```css:css
/* デフォルトの親要素スタイル */
.hover-container {
  background: white;
  height: 100vh;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* ボタン自体のスタイル */
.hover-container button {
  padding: 20px 40px;
  font-size: 1rem;
  color: #fff;
  background: #333;
  border: none;
  cursor: pointer;
}

/* 子要素 button をホバーしているときのみ親要素に適用 */
.hover-container:has(button:hover) {
  background: #0000ff;  /* 青背景 */
}
```
