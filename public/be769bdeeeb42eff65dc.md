---
title: 【Mac】カーソルの「A」や「あ」を非表示にする方法【Sonoma】
tags:
  - Mac
private: false
updated_at: '2024-04-01T02:29:09+09:00'
id: be769bdeeeb42eff65dc
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Somomaでは、キーボードの言語を切り替えた際に現在の入力言語を示すインジケータがテキストカーソルに表示されます。

![スクリーンショット 2024-04-01 2.04.28.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/d252db1d-890c-bfad-8945-1fd66fa097b7.png)

このインジケータを非表示にする方法について記載します。

## 非表示にする方法

ターミナルで以下のコマンドを実行します。

```terminal
defaults write kCFPreferencesAnyApplication TSMLanguageIndicatorEnabled 0
```

コマンドを実行した際に起動されていたアプリケーションではまだインジケータが表示されます。

![スクリーンショット 2024-04-01 2.01.40.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/048b42ee-61a8-a84d-88bc-d4bdb500e3b7.png)

アプリケーションを再起動するとインジケータが表示されなくなります。

:::note warn
Caps Lockがオンになっている時にはインジケータが表示されます。
:::

## 再表示したい場合

再表示する場合には以下のコマンドを実行します。

```terminal
defaults write kCFPreferencesAnyApplication TSMLanguageIndicatorEnabled 1
```

## 参考

https://www.alfredforum.com/topic/21080-alfred-doesnt-show-the-text-cursor-in-macos-sonoma-if-the-redesigned-text-cursor-is-disabled/#comment-109517
