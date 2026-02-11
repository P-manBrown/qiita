---
title: 【Zed】初期プロンプト付きでエージェントパネルを開く方法
tags:
  - ZedEditor
private: false
updated_at: '2026-02-11T23:14:33+09:00'
id: d72b68a711ca04455b92
organization_url_name: null
slide: false
ignorePublish: false
---
## 概要

Zed v0.223.0以降では、`zed://agent` URLスキーマを使用して、事前に入力されたプロンプトでエージェントパネルを開くことができるようになりました。

## 使用方法

### 基本構文

```
zed://agent?prompt=<URLエンコードされたテキスト>
```

### 使用例

```
zed://agent?prompt=Hello%20World
```

このURLを開くと、「Hello World」というプロンプトが入力された状態でエージェントパネルが開きます。

## 参考

https://github.com/zed-industries/zed/pull/47959
