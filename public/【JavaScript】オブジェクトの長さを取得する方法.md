---
title: 【JavaScript】オブジェクトの長さを取得する方法
tags:
  - 'JavaScript'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 取得方法

```javascript
const user = {
  name: "田中太郎",
  age: 30,
  email: "tanaka@example.com"
};

console.log(Object.keys(user).length); // 3
```

`Object.keys()`はオブジェクトの列挙可能なプロパティ名の配列を返し、その配列の長さでプロパティ数がわかります。

## 参考

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys
