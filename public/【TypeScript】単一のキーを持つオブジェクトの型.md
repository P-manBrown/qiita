---
title: 【TypeScript】単一のキーを持つオブジェクトの型
tags:
  - 'typescript'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

以下のように型を定義すると単一のキーを持つオブジェクトを判定できます。

```typescript
type UnionToIntersection<U> =
  (U extends any ? U : never) extends ((k: infer I) => void)
    ? I
    : never;

type IsUnion<T> = [T] extends [UnionToIntersection<T>] ? false : true;

type SingleKey<T> = IsUnion<keyof T> extends true
  ? never
  : {} extends T
  ? never
  : T;

```

```typescript
// Union型 U の各要素を Intersection 型に変換する型定義
// 分配条件型と関数型の引数推論を利用して、Union を Intersection に変換する
type UnionToIntersection<U> =
// U extends any ? U : never によってUnionの各要素に分配し、
// その結果を関数型 ((k: infer I) => void) のパラメータに当てはめ、
// infer I により Intersection 型として推論する
  (U extends any ? U : never) extends ((k: infer I) => void)
    ? I // 推論された Intersection 型を返す
    : never;

// 型 T が Union であるかどうか判定する型定義
// Unionでない場合、UnionToIntersection<T> と [T] の型が一致するため false を返す
type IsUnion<T> = [T] extends [UnionToIntersection<T>] ? false : true;

// オブジェクト型 T が「単一のキー」を持つかをチェックする型定義
// ・keyof T が Union なら複数のキーが存在するため never を返す
// ・空のオブジェクトの場合 ({} extends T) も許容しないため never を返す
// それ以外の場合に限り T を返す
type SingleKey<T> = IsUnion<keyof T> extends true
  ? never
  : {} extends T
  ? never
  : T;

// T は Record<string, any> を継承しており、obj 引数は SingleKey<T> 型（単一キーかつ空でないオブジェクト）であることを要求する
function sample<T extends Record<string, any>>(obj: SingleKey<T>) {
  console.log({ obj });
}

// 空のオブジェクトは {} extends T の判定で never となるためエラーになる
sample({}); // エラー

// 単一のキーのオブジェクトは許容される
sample({ test: 5 }); // OK

// 複数のキーを持つため、keyof T が Union となり、never となるためエラーになる
sample({ test: 5, example: 6 }); // エラー

```
