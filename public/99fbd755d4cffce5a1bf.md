---
title: 【React】イミュータビリティを実現する方法【JavaScript】
tags:
  - JavaScript
  - React
  - 初学者
private: false
updated_at: '2023-01-13T18:13:44+09:00'
id: 99fbd755d4cffce5a1bf
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに
　本記事は、プログラミング初学者が、学習を進めていて疑問に思った点について調べた結果を備忘録も兼ねてまとめたものです。
　そのため、記事の内容に誤りが含まれている可能性があります。ご容赦ください。
　間違いを見つけた方は、お手数ですが、ご指摘いただけますと幸いです。

## 今回の疑問点
　今回の疑問点は、

　　_Reactにおけるイミュータビリティを実現する方法_
　
　です。　

以前、[Reactチュートリアル](https://ja.reactjs.org/tutorial/tutorial.html)に取り組んでいた際に、その中でイミュータビリティの重要性について解説されていました。また、以下のような文章も記載がありましたが、イミュータビリティの実現方法については、理解が不十分だと思い、調べることとしました。
>push() メソッドの方に慣れているかもしれませんが、それと違って concat() は元の配列をミューテートしないため、こちらを利用します。

## 疑問点に対する解説

### イミュータビリティとは
イミュータビリティとは、不変性を意味します。
データを直接書き換えるのではなく、望む変更を加えた新しいデータのコピーで古いデータを置き換えることで実現できます。
具体的には、以下のようなものはミュータブルなアプローチ、

```mutable.js
// ミュータブルなアプローチ
var person = {age: 18, name: 'Taro'};
person.age = 22;
//anotherPerson は {age: 22, name: 'Taro'} に改変される
```
以下のようなものがイミュータブルなアプローチとなります。

```immutable.js
// イミュータブルなアプローチ
var person = {age: 18, name: 'Taro'};

var anotherPerson = {...person, age: 22};
// person に変化はなし, 一方で anotherPerson は {age: 22, name: 'Taro'}
```

### イミュータビリティの重要性
イミュータビリティの重要性については、[Reactチュートリアル](https://ja.reactjs.org/tutorial/tutorial.html#why-immutability-is-important)に詳細な説明があります。
また、Reactチュートリアルに取り組むことでその重要性を体感することができます。

### イミュータビリティを実現する方法
配列を操作する際にイミュータビリティについて特に留意する必要があります。
JavaScriptにおける配列操作には、破壊的なものと非破壊的なものがあります。
破壊的なメソッドの具体例は以下の通りです。

- splice()
- copyWithin()
- fill()
- pop()
- push()
- shift()
- unshift()
- reverse()
- sort()

上述の破壊的、非破壊的という分類がミュータブル、イミュータブルという分類に対応しています。
すなわち、列挙した破壊的なメソッドの使用は避け、非破壊的なメソッドを使用するようにすることでイミュータビリティを実現することができます。
具体例は以下の通りです。

#### 要素の追加
push()やunshift()は使わず、スプレッド構文を使用することで実現します。

```sample.js
const numbers = [1, 2, 3]

const newNumbers = [...numbers, 4]
console.log(newNumbers)
// [1, 2, 3, 4]
```

#### 要素の削除
破壊的なpop()やshift()、splice()は使わず、filter()を使用することで実現します。

```sample.js
const numbers = [ "one", "two", "three"]

const newNumbers = numbers.filter(number => number !== "two")
console.log(newNumbers)
// ["one", "three"]
```

#### 配列の加工
map()又はreduce()を使用することで実現します。

```map.js
var numbers = [1, 4, 9, 16];
const newNumbers = numbers.map(x => x * 2);
console.log(newNumbers);
// [2, 8, 18, 32]

const numbers = [1, 2, 3, 4, 5]
const editNumber = (oldNumber, newNumber, arr) =>
   arr.map(number => (number === oldNumber) ? newNumber : number)
const updatedNumbers = editNumber(3, 100, numbers)
console.log(updatedNumbers)
// [1, 2, 100, 4, 5]
```

```reduce.js
const numbers = [15, 24, 13, 35]
const max = numbers.reduce(
  (max, value) => (value > max) ? value : max, 0)
console.log('max', max);
// max 35

const numbers = ["one", "one", "two", "three", "two"];
const distinctNumbers = numbers.reduce(
  (distinct, number) =>
    (distinct.indexOf(number) !== -1) ?  
     distinct 
     : 
     [...distinct, number],[]
    )
console.log(distinctNumbers)
// ["one", "two", "three"]

```

#### 破壊的なメソッドを使用したいとき
reverse()やsort()等、どうしても破壊的メソッドを使いたい場合には、スプレッド構文等で変更を加えたい配列のコピーを作成し、このコピーに対して変更を行うことで実現します。

```sample.js
const numbers = [3, 2, 1]

const newNumbers = Array.from(numbers).sort();
console.log(newNumbers);
// [1, 2, 3]
```

## まとめ

- イミュータビリティは、破壊的メソッドの使用を避け、非破壊的メソッドを使用することで実現することができる
- 配列の操作の際には、特に注意が必要
