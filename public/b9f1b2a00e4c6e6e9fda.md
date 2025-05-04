---
title: 【cron】使用するシェルを変更する方法
tags:
  - cron
  - crontab
  - 初学者
private: false
updated_at: '2022-09-19T12:32:06+09:00'
id: b9f1b2a00e4c6e6e9fda
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法
`crontab`に以下のように記述することで変更できます。
デフォルトは sh です。
```zsh
SHELL=/bin/zsh
* * * * * echo $0 > test.log 
```

```test.log
/bin/zsh
```
