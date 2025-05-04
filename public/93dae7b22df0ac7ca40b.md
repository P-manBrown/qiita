---
title: >-
  【Docker】sed: couldn't open temporary file ./sedxxx: Permission denied
  対処法【VirtioFS】
tags:
  - Docker
  - docker-compose
  - 初学者
  - VirtioFS
private: false
updated_at: '2023-03-03T04:02:45+09:00'
id: 93dae7b22df0ac7ca40b
organization_url_name: null
slide: false
ignorePublish: false
---
## 状況

Dockerでファイル共有にVirtioFSを使用してコンテナ内で`sed -i`を実行したところ以下のようなエラーが出ました。

```terminal
$ sed -i 's/example/EXAMPLE/' sample.txt
sed: couldn't open temporary file ./sedxxx: Permission denied
```

## 対処法

次のようにバインドマウントをしていないディレクトリにファイルをコピーします。
その後そのファイルに対して`sed -i`を実行しオリジナルのファイルにその内容をコピーして戻します。

```terminal
$ cp ./sample.txt /tmp/sample.txt
$ sed -i 's/example/EXAMPLE/' /tmp/sample.txt
$ cp -f /tmp/sample.txt ./sample.txt
```

または次のように`-i`オプションを使用しないようにします。

```terminal
$ sed 's/example/EXAMPLE/' ./sample.txt > ./sample.txt.tmp
$ mv -f ./sample.txt.tmp ./sample.txt
```

## 参考

https://forums.docker.com/t/sed-couldnt-open-temporary-file-xyz-permission-denied-when-using-virtiofs/125473
