---
title: '【TypeScript】アクセス修飾子 '
tags:
  - TypeScript
  - 初学者
private: false
updated_at: '2022-06-13T02:40:00+09:00'
id: dee35e0bd3c9fecf18bc
organization_url_name: null
slide: false
ignorePublish: false
---
## アクセス修飾子とは
アクセス修飾子を使用することでメンバのアクセス範囲を限定することができます。
アクセス修飾子には`public`, `private`, `protected`があります。
| アクセス修飾子 | 範囲 |
|:-:|:- |
| なし         | publicと同様  |
| public      | どこからでもアクセス可能  |
| private     | クラス内のみアクセス可能   |
| protected   | クラス内とサブクラスからアクセス可能 |

## public
``` ts
class Person { 
  // publicは省略可
  public name: string
  public age: number
  constructor(name: string, age: number) {
    this.name = name
    this.age = age
  }
  profile(): string {
    return `name: ${this.name}, age: ${this.age}`
  }
}

let tanaka = new Person("Tanaka", 32)
console.log(tanaka.profile())
// > name: Tanaka, age: 32
// public のため参照可能
```

## private
```ts
class Person {
  public name: string
  // private　に変更
  private age: number
  constructor(name: string, age: number) {
    this.name = name
    this.age = age
  }
  profile(): string {
    return `name: ${this.name}, age: ${this.age}`
  }
}

let tanaka = new Person("Tanaka", 32)
console.log(tanaka.profile())
//  > name: Tanaka, age: 32
// Profile 内のため参照可能
console.log(tanaka.name)
// > Tanaka
// public のため参照可能
console.log(tanaka.age)
// > error TS2341: Property 'age' is private and only accessible within class 'Person'.
// Person 外のため参照不可
```

## protected
```ts
class Person {
  public name: string
  // public　に変更
  public age: number
  // protected を追加
  protected nationality: string
  constructor(name: string, age: number, nationality: string) {
    this.name = name
    this.age = age
    this.nationality = nationality
  }
  profile(): string {
    return `name: ${this.name}, age: ${this.age}`
  }
}

class Android extends Person {
  constructor(name: string, age: number, nationality: string) {
    super(name, age, nationality)
  }
  profile(): string {
    return `name: ${this.name}, age: ${this.age}, nationality: ${this.nationality}`
  }
}

let kato = new Android("kato", 24, "Japan")
console.log(kato.nationality)
// > error TS2445: Property 'nationality' is protected and only accessible within class 'Person' and its subclasses.
// Preson 内でも Android 内でもないため参照不可
console.log(kato.profile())
// > name: kato, age: 24, nationality: Japan
// Android 内のため参照可能
```
