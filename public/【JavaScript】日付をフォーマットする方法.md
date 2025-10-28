---
title: 【JavaScript】日付をフォーマットする方法
tags:
  - JavaScript
private: false
updated_at: '2025-10-28T22:50:49+09:00'
id: 7a04957e750a4207e3e2
organization_url_name: null
slide: false
ignorePublish: false
---
## 手動フォーマット

最も基本的な方法は、`Date`オブジェクトのメソッドを使って手動でフォーマットする方法です。

```javascript
const date = new Date();
const year = date.getFullYear();
const month = ('0' + (date.getMonth() + 1)).slice(-2); // ゼロ埋め
const day = ('0' + date.getDate()).slice(-2); // ゼロ埋め

const formattedDate = `${year}-${month}-${day}`;
console.log(formattedDate); // 例: 2024-12-28
```

## toLocaleDateString()

ロケールに応じた日付表示が簡単にできるメソッドです。

```javascript
const date = new Date();

// 基本的な使い方
console.log(date.toLocaleDateString('ja-JP')); // 例: 2024/12/28

// オプションでカスタマイズ
const options = { 
  year: 'numeric', 
  month: '2-digit', 
  day: '2-digit' 
};
console.log(date.toLocaleDateString('ja-JP', options)); // 例: 2024/12/28
```

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleDateString

##  Intl.DateTimeFormat

最も柔軟で強力な国際化対応の日付フォーマット機能です。

```javascript
const date = new Date();

// 詳細な日付表示
const formatter = new Intl.DateTimeFormat('ja-JP', { 
  dateStyle: 'full' 
});
console.log(formatter.format(date)); // 例: 2024年12月28日土曜日

// カスタムフォーマット
const customFormatter = new Intl.DateTimeFormat('ja-JP', {
  year: 'numeric',
  month: 'long',
  day: 'numeric',
  weekday: 'short'
});
console.log(customFormatter.format(date)); // 例: 2024年12月28日(土)
```

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat
