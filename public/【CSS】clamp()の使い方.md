---
title: 【CSS】clamp()の使い方
tags:
  - 'CSS'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
`clamp()` は CSS で値を **最小値**・**推奨値**・**最大値** の範囲内に収めるための関数です。

## `clamp()` の基本構文

```css
clamp(minimum, recommended, maximum)
```

- `minimum`：最小値。これより小さくはならない。  
- `recommended`：推奨値。通常はこちらが適用される。  
- `maximum`：最大値。これより大きくはならない。

## 例

```css
.card {
  width: clamp(200px, 50vw, 400px);
  padding: 1rem;
  background: #f5f5f5;
  border-radius: 8px;
}
```

- ビューポート幅が狭いときは最低幅 200px  
- 推奨は画面幅の 50%  
- 広大な画面では最大幅 400px
