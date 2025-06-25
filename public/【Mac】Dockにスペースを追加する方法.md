---
title: 【Mac】Dockにスペースを追加する方法
tags:
  - 'Mac'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## スペースを追加するコマンド

以下のコマンドを実行するとDockにスペースが追加されます。

```terminal
defaults write com.apple.dock persistent-apps -array-add '{tile-data={}; tile-type="spacer-tile";}' && killall Dock
```

## 移動する

ドラッグ・アンド・ドロップでスペースの場所を変更できます。

![screen-recording-69.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/780fb731-6dc9-4a0f-9769-2528dcbdb3f9.gif)

## 削除する

削除するにはスペースを右クリックして`Dockから削除`をクリックします。

![screen-recording-70.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/f6effcea-1734-4f4d-aaf0-c084d6516554.gif)
