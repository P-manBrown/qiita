---
title: 【JavaScript】map()とforEach()の使い分け
tags:
  - JavaScript
private: false
updated_at: '2026-02-01T23:53:14+09:00'
id: 02d9b5c08a9aabfa42bb
organization_url_name: null
slide: false
ignorePublish: false
---
## map()

`map()`メソッドは、配列の各要素に指定された関数を適用し、その結果から新しい配列を作成します。データの変換や加工によく使用されます。

### 構文

```javascript
map((currentElement, indexOfElement, array) => { ... });
```

### 例

```javascript
const numbers = [1, 2, 3, 4];

const doubledNumbers = numbers.map((number) => {
  return number * 2;
});

console.log(doubledNumbers);
// [2, 4, 6, 8]
```

## forEach()

`forEach()`メソッドは、配列の各要素に対して指定された関数を一度ずつ実行します。ログ出力や要素の直接変更などの操作に適しています。

### 構文

```javascript
array.forEach(callback(currentValue, index, array), thisArg);
```

### 例

```javascript
const numbers = [1, 2, 3, 4];

numbers.forEach((number) => {
  console.log(number * 2);
});

// 出力:
// 2
// 4
// 6
// 8
```

## 主な違い

| 項目             | forEach()        | map()                            |
| ---------------- | ---------------- | -------------------------------- |
| 戻り値           | `undefined`      | 新しい配列                       |
| 用途             | 副作用を伴う処理 | データの変換                     |
| メソッドチェーン | 不可             | 可能（`reduce()`, `sort()`など） |

## どちらを使うべきか

- **forEach()を使う場合**: 配列を単に繰り返し処理したい場合や、変換を必要としない処理（コンソール出力、DOM操作など）
- **map()を使う場合**: 配列の各要素を変換して新しい配列を作成したい場合や、後続のメソッドをチェーンしたい場合

## 参考

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map
