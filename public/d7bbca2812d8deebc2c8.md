---
title: 【Bash】変数の値から指定したパターンに前方一致した部分を削除する方法
tags:
  - Bash
private: false
updated_at: '2024-09-04T23:54:57+09:00'
id: d7bbca2812d8deebc2c8
organization_url_name: null
slide: false
ignorePublish: false
---
変数展開の際に以下のように記述すると変数内の値から指定したパターンに前方一致（最短一致）した部分を削除できます。

```sample.sh
SAMPLE=path/to/SAMPLE

echo ${SAMPLE#path}

```

```sample.sh
SAMPLE=path/to/SAMPLE

echo ${SAMPLE#path}

```

```terminal
$ bash sample.sh
/to/SAMPLE
```

`path/to/SAMPLE`から`path`が削除されています。
