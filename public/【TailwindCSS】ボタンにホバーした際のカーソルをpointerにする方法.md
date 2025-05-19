---
title: 【TailwindCSS】ボタンにホバーした際のカーソルをpointerにする方法
tags:
  - 'tailwindcss'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

## v4では`button`の`cursor`は`default`

v4では`button`の`cursor`が`pointer`から`default`に変更されました。
よって、ボタンにホバーした際にカーソルがpointerになりません。

## すべての`button`の`cursor`を`pointer`にする

`global.css`に以下の記述を追加することですべての`button`と`role="button"`の要素（`disabled`を除く）の`cursor`が`pointer`に設定されます。
これにより、ボタンにホバーした際にカーソルがpointerになるようになります。

```css:global.css
@layer base {
  button:not(:disabled),
  [role="button"]:not(:disabled) {
    cursor: pointer;
  }
}
```

## 参考

https://tailwindcss.com/docs/upgrade-guide#buttons-use-the-default-cursor
