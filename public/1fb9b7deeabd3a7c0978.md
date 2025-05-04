---
title: 【Ruby】ユーザの入力を受け付ける方法
tags:
  - Ruby
private: false
updated_at: '2024-09-22T19:55:47+09:00'
id: 1fb9b7deeabd3a7c0978
organization_url_name: null
slide: false
ignorePublish: false
---
ユーザーからの入力を受け付けるには`gets`メソッドを使用します。

## 基本的な使い方

`gets`メソッドは、標準入力から1行のデータを読み取ります。
以下は、`gets`メソッドの基本的な使用例です。

```ruby:example.rb
puts "名前を入力してください"

name = gets

puts "こんにちは" + name + "さん"
```

このコードを実行すると、ユーザーに名前の入力を促し、入力された文字列を使用してメッセージを出力します。

```terminal
$ ruby example.rb
名前を入力してください
sample
こんにちはsample
さん
```

## 改行文字の取り扱い

`gets`メソッドは、入力されたデータの末尾に改行文字を含みます。
この改行文字は`chomp`メソッドを使用することで削除できます。

```ruby
puts "名前を入力してください"

name = gets.chomp

puts "こんにちは" + name + "さん"
```

上記のようにすることで末尾の改行文字が削除されます。

```terminal
$ ruby example.rb
名前を入力してください
sample
こんにちはsampleさん
```

