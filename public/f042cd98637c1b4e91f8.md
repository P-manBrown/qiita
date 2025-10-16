---
title: 【JavaScript】文字列をブール値に変換する方法
tags:
  - JavaScript
private: false
updated_at: '2025-06-07T22:45:58+09:00'
id: f042cd98637c1b4e91f8
organization_url_name: null
slide: false
ignorePublish: false
---

## `===`を使用する

`===`で文字列が`true`か判定します。大文字と小文字が区別されるため、`toLowerCase()`が必要な場合があります。

```javascript
const boolString = "True"
const boolValue = (boolString.toLowerCase() === "true")
console.log(boolValue) // true
```

## 正規表現を使用する

以下のように正規表現を使用して文字列が`true`か判定します。

```javascript
const boolString = "true"
const boolValue = (/true/).test(boolString)
console.log(boolValue) // true
```

大文字と小文字を区別しない場合には次のようにします。

```javascript
const boolString = "True"
const boolValue = (/true/i).test(boolString)
console.log(boolValue) // true
```

## `!!`を使用する

この方法は上記2つとは異なり、空文字か否かを判定します。

```javascript
const stringValue1 = !!'true'
const stringValue2 = !!''

console.log(stringValue1) // true
console.log(stringValue2) // false
```

## `Boolean()`を使用する

この方法も空文字か否かを判定します。

```javascript
const stringValue1 = Boolean('true')
const stringValue2 = Boolean('')

console.log(stringValue1) // true
console.log(stringValue2) // false
```
