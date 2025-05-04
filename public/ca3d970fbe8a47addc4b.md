---
title: 【CSS】imgの代替テキストを装飾する方法
tags:
  - CSS
private: false
updated_at: '2023-11-17T23:57:24+09:00'
id: ca3d970fbe8a47addc4b
organization_url_name: null
slide: false
ignorePublish: false
---
以下のように`img`にテキストに対するCSSを記述することで代替テキストを装飾できます。

色を変更するには以下のように`color`を設定します。

```html
<img class="sample" src="sample.jpg" alt="サンプル" height="100" width="100">
```

```css
.sample{
  display:block;
  border : 1px solid black;
  background-color:black;
  color:red;
}
```
