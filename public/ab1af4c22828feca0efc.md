---
title: ' 【Linux】一度に複数のファイルを作成する方法'
tags:
  - Linux
  - Linuxコマンド
  - 初学者
private: false
updated_at: '2023-02-02T23:51:56+09:00'
id: ab1af4c22828feca0efc
organization_url_name: null
slide: false
ignorePublish: false
---

## 複数ファイルを扱う方法
以下のように`{}`で括り、`,`で区切ることで複数ファイルを扱うことができます。
```
{file1,file2}
```

### `touch`コマンド
```
$ touch {index.html,style.css}
```

### `mkdir`コマンド
```
$ mkdir {dir1,dir2}
$ touch {dir1/index.html,dir2/style.css}
```

