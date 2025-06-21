---
title: 【Mac】Spotlightのインデックスを再構築する方法
tags:
  - 'Mac'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
次のコマンドを実行してインデックスを再構築できます。

```shell
sudo mdutil -E /
```

インデックスを一度無効化しても再構築されます。

```shell
sudo mdutil -a -i off && sudo mdutil -a -i on
```
