---
title: 【Mac】shutdownコマンドの使い方
tags:
  - 'Mac'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

##  すぐにシャットダウン

```terminal
sudo shutdown -h now
```

## すぐにスリープ

```terminal
sudo shutdown -s now
```

## すぐに再起動

```terminal
sudo shutdown -r now
```

## 10分後に再起動

```terminal
sudo shutdown -r "+10"
```

## 午後2時にシャットダウン

```terminal
sudo shutdown -h 1400
```

## 2025年5月10日午前11時30分にリブート（入力フォーマット：YYMMDDHHMM）

```terminal
sudu shutdown -r 2505101130
```

## 参考

https://keith.github.io/xcode-man-pages/shutdown.8.html

