---
title: 【JavaScript】連続した数字の配列を生成する方法
tags:
  - JavaScript
private: false
updated_at: '2025-07-29T23:05:51+09:00'
id: abc7ae915d09cea904c9
organization_url_name: null
slide: false
ignorePublish: false
---
## 生成方法

`Array.from()`を使用して連続した数字の配列を生成できます。

```javascript
const sample = Array.from({ length: 10 }, (_, i) => i)
console.log(sample) [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

`1`から`15`までの配列を生成するには以下のようにします。

```javascript
const sample = Array.from({ length: 15 }, (_, i) => i + 1)
console.log(sample) [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
```

## 参考

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from
