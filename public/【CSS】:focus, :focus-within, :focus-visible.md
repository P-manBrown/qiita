---
title: '【CSS】:focus, :focus-within, :focus-visible'
tags:
  - CSS
private: false
updated_at: '2025-08-03T21:58:11+09:00'
id: 7af8b6b4983053f53bd1
organization_url_name: null
slide: false
ignorePublish: false
---
## `:focus` - 基本的なフォーカス状態

```css
input:focus {
  border: 2px solid blue;
}
```

- 要素がフォーカスを受けた時に適用される最も基本的な疑似クラスです
- キーボード操作（Tabキー）、マウスクリック、プログラム的な操作すべてで適用されます
- 全てのフォーカス状態をカバーします

## `:focus-visible` - 視覚的フォーカス表示が適切な場合

```css
button:focus-visible {
  outline: 2px solid orange;
}
```

- ブラウザーが「ユーザーがフォーカス表示を必要としている」と判断した場合のみ適用されます
- 一般的にキーボード操作では適用され、マウスクリックでは適用されません

## `:focus-within` - 子要素を含むフォーカス状態

```css
form:focus-within {
  background-color: #f0f0f0;
}
```

- その要素または子要素のいずれかがフォーカスを受けている時に適用されます
- 親要素のスタイルを子要素のフォーカス状態に応じて変更可能です

## 参考

https://developer.mozilla.org/ja/docs/Web/CSS/:focus

https://developer.mozilla.org/ja/docs/Web/CSS/:focus-visible

https://developer.mozilla.org/ja/docs/Web/CSS/:focus-within
