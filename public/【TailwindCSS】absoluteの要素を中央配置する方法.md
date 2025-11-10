---
title: 【TailwindCSS】absoluteの要素を中央配置する方法
tags:
  - tailwindcss
private: false
updated_at: '2025-11-10T22:24:14+09:00'
id: 902dee8abb80ee3fb1c4
organization_url_name: null
slide: false
ignorePublish: false
---
## Flexboxを使用

親要素に`flex`、`items-center`、`justify-center`を適用し、absolute要素を`inset-0`で配置します。

```html
<div class="relative w-80 h-80">
  <div class="absolute inset-0 flex items-center justify-center">
    <button class="bg-blue-500 text-white px-6 py-3 rounded">
      中央配置
    </button>
  </div>
</div>
```

## top-1/2とleft-1/2を使用

`top-1/2 left-1/2`で要素を50%の位置に配置し、`-translate-x-1/2 -translate-y-1/2`で要素自身のサイズ分だけ戻します。

```html
<div class="relative w-80 h-80">
  <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2">
    <button class="bg-green-500 text-white px-6 py-3 rounded">
      中央配置
    </button>
  </div>
</div>
```

## Grid Layoutを使用

親要素に`grid place-items-center`を適用することで中央配置できます。

```html
<div class="relative w-80 h-80 grid place-items-center">
  <div class="absolute">
    <button class="bg-purple-500 text-white px-6 py-3 rounded">
      中央配置
    </button>
  </div>
</div>
```
