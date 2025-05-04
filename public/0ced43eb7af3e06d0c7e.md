---
title: 【Linux】乱数の生成方法
tags:
  - Linux
private: false
updated_at: '2023-08-04T23:54:08+09:00'
id: 0ced43eb7af3e06d0c7e
organization_url_name: null
slide: false
ignorePublish: false
---
## 生成方法

`RANDOM`変数を使用することで乱数を生成できます。  
`RANDOM`変数は`0`から`32767`の間の数値を返却します。  

```terminal
$ echo $RANDOM
18739
```

数値の範囲を`0`から`9`までにしたい場合には以下のように実行します。  

```terminal
$ echo $(($RANDOM % 10))
4
$ echo $(($RANDOM % 10))
6
$ echo $(($RANDOM % 10))
0
$ echo $(($RANDOM % 10))
5
$ echo $(($RANDOM % 10))
7
$ echo $(($RANDOM % 10))
8
```

数値の範囲を`1`から`10`までにしたい場合には以下のように実行します。  

```terminal
$ echo $(($RANDOM % 10 + 1))
2
$ echo $(($RANDOM % 10 + 1))
4
$ echo $(($RANDOM % 10 + 1))
10
$ echo $(($RANDOM % 10 + 1))
9
$ echo $(($RANDOM % 10 + 1))
7
```

数値の範囲を`101`から`200`にしたい場合には以下のように実行します。  

```terminal
$ echo $(($RANDOM % 100 + 101))
195
$ echo $(($RANDOM % 100 + 101))
139
$ echo $(($RANDOM % 100 + 101))
101
$ echo $(($RANDOM % 100 + 101))
148
$ echo $(($RANDOM % 100 + 101))
142
```
