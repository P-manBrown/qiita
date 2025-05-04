---
title: 【Linux】複数のファイルを重複行を削除してマージする方法
tags:
  - Linuxコマンド
private: false
updated_at: '2025-02-22T23:56:17+09:00'
id: 532a7fad0519dcdcf0ae
organization_url_name: null
slide: false
ignorePublish: false
---
以下のようにコマンドを実行すると複数ファイルを重複行を削除してマージできます。

```terminal
cat a.txt b.txt c.txt | awk '!seen[$0]++' > abc.txt
```
