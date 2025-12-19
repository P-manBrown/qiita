---
title: 【JavaScript】Dateオブジェクトを日付と時刻に分割する方法
tags:
  - JavaScript
private: false
updated_at: '2025-12-19T20:23:46+09:00'
id: 9dc4a29eefe1881537ae
organization_url_name: null
slide: false
ignorePublish: false
---
## 分割方法

```javascript
const now = new Date();

// 日付部分を取得（YYYY-MM-DD形式）
const datePart = `${now.getFullYear()}-${(now.getMonth() + 1).toString().padStart(2, '0')}-${now.getDate().toString().padStart(2, '0')}`;

// 時刻部分を取得（HH:MM:SS形式）
const timePart = `${now.getHours().toString().padStart(2, '0')}:${now.getMinutes().toString().padStart(2, '0')}:${now.getSeconds().toString().padStart(2, '0')}`;

console.log('Date:', datePart); // Date: 2024-12-19
console.log('Time:', timePart); // Time: 14:30:45
```

## 使用するメソッド

- `getFullYear()`: 年を取得
- `getMonth()`: 月を取得（0-11なので+1が必要）
- `getDate()`: 日を取得
- `getHours()`: 時を取得
- `getMinutes()`: 分を取得
- `getSeconds()`: 秒を取得

`getMonth()`は0から11の値を返すため、表示時には+1する必要があります。
```javascript
// ❌ 間違い
const month = now.getMonth();

// ✅ 正しい
const month = now.getMonth() + 1;
```

時刻や日付が1桁の場合に`padStart(2, '0')`でゼロ埋めします。

```javascript
// ❌ 間違い（9時が"9:5:3"になる）
const timePart = `${now.getHours()}:${now.getMinutes()}:${now.getSeconds()}`;

// ✅ 正しい（9時が"09:05:03"になる）
const timePart = `${now.getHours().toString().padStart(2, '0')}:${now.getMinutes().toString().padStart(2, '0')}:${now.getSeconds().toString().padStart(2, '0')}`;
```

## 参考

https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Date
