---
title: 【Linux】sedでスペースを含む文字列を追加する方法
tags:
  - Linuxコマンド
private: false
updated_at: '2024-08-28T23:49:20+09:00'
id: fda2c8f2c2390adb00dd
organization_url_name: null
slide: false
ignorePublish: false
---
追加する文字列にスペースを追加するには以下のようにします。  

```terminal
sed -i "/text/a \          追加するテキスト" sample.txt
```

```sample.txt
text
          追加テキスト
```
