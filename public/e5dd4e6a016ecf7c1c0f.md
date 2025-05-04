---
title: 【Linux】コマンドでアーカイブを作成・展開する方法
tags:
  - Linuxコマンド
private: false
updated_at: '2024-08-22T23:51:13+09:00'
id: e5dd4e6a016ecf7c1c0f
organization_url_name: null
slide: false
ignorePublish: false
---
## アーカイブの作成
```:ターミナル
$  tar cvf アーカイブ名 対象ファイル1 対象ファイル2　...
```
```:ターミナル
$ tar cvf sample.tar test_1.txt test_2.txt
```

## アーカイブの展開
```:ターミナル
$  tar xvf アーカイブ名 対象ファイル1 対象ファイル2　...
```

```:ターミナル
$ tar xvf sample.tar
```
