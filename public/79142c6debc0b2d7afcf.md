---
title: シェルスクリプトに引数を渡す方法
tags:
  - shell
  - 初学者
private: false
updated_at: '2022-12-11T21:57:02+09:00'
id: 79142c6debc0b2d7afcf
organization_url_name: null
slide: false
ignorePublish: false
---
## 引数を渡す方法

以下の内容で`sample.sh`を作成します。  

```sample.sh
echo "引数: $@"

echo "引数1: $1"
echo "引数2: $2"
echo "引数3: $3"
```

ターミナルで次のようにコマンドを実行すると引数を渡せます。  

```terminal
 bash sample.sh arg1 arg2 arg3
```

```terminal
$ bash sample.sh arg1 arg2 arg3
引数: arg1 arg2 arg3
引数1: arg1
引数2: arg2
引数3: arg3
```
