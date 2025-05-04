---
title: 【npm】package.jsonのバージョンの指定方法【yarn】
tags:
  - npm
  - package.json
  - YARN
private: false
updated_at: '2023-06-02T05:31:54+09:00'
id: a2febf23f12854cddb4f
organization_url_name: null
slide: false
ignorePublish: false
---
## 特定のバージョンを指定
`1.2.3`のように記述するとバージョン1.2.3で固定できます。

```json:package.json
{
  "name": "sample-app",
  "dependencies": {
    "sample": "1.2.3"
  }
}
```

## 指定バージョンより最新

`>1.2.3`のように記述するとバージョン1.2.3よりも大きいバージョンの内、最新のものがインストールされます。
上記の場合にバージョン2.0.0が出た場合には2.0.0にアップグレードされます。

```json:package.json
{
  "name": "sample-app",
  "dependencies": {
    "sample": ">1.2.3"
  }
}
```

## 指定したバージョン以上の最新
`>=1.2.3`のように記述すると、バージョン1.2.3以上のバージョンで最新のものがインストールされます。
上記の場合にバージョン2.0.0が出た場合には2.0.0にアップグレードされます。

```json:package.json
{
  "name": "sample-app",
  "dependencies": {
    "sample": ">=1.2.3"
  }
}
```

## 指定したバージョン未満の最新
`<1.2.3`のように記述すると、バージョン1.2.3未満で最新のバージョンがインストールされます。

```json:package.json
{
  "name": "sample-app",
  "dependencies": {
    "sample": "<1.2.3"
  }
}
```

## 指定したバージョン以下の最新
`<=1.2.3`のように記述すると、バージョン1.2.3以下の最新のバージョンがインストールされます。

```json:package.json
{
  "name": "sample-app",
  "dependencies": {
    "sample": "<=1.2.3"
  }
}
```

## バグ修正のみ取り込む

`~1.2.3`のように記述すると、バージョン1.2.3のパッチバージョンが最新のバージョンがインストールされます。

```json:package.json
{
  "name": "sample-app",
  "dependencies": {
    "sample": "~1.2.3"
  }
}
```


## 指定したメジャーバージョンの最新

`^1.2.3`のように記述すると、バージョン1.2.3以上でメジャーバージョンが1の最新のバージョンがインストールされます。

```json:package.json
{
  "name": "sample-app",
  "dependencies": {
    "sample": "^1.2.3"
  }
}
```

## 一部をワイルドカードで指定

`1.2.x`のように記述すると、バージョン1.2の中でパッチバージョンが最新のバージョンがインストールされます。

```json:package.json
{
  "name": "sample-app",
  "dependencies": {
    "sample": "1.2.x"
  }
}
```

## 最新バージョン
`*`を記述するかバージョンを指定しないと、最新のバージョンがインストールされます。

```json:package.json
{
  "name": "sample-app",
  "dependencies": {
    "sample": "*".
    "example": ""
  }
}
```

## 範囲指定

`1.2.3 - 2.0.0`のように記述すると、指定されたバージョンの範囲で最新のバージョンがインストールされます。

```json:package.json
{
  "name": "sample-app",
  "dependencies": {
    "sample": "1.2.3 - 2.0.0"
  }
}
```
