---
title: 【Mac】AppleScriptで通知センターの通知をすべて削除する方法
tags:
  - Mac
private: false
updated_at: '2025-06-15T13:42:15+09:00'
id: f7fe4b22453c49a32f3b
organization_url_name: null
slide: false
ignorePublish: false
---

## 通知センターで通知をすべて削除するAppleScript

```applescript
tell application "System Events" to tell application process "NotificationCenter"
    -- 通知センターのウィンドウ内にある最初のグループ（targetGroup）を取得
    set targetGroup to group 1 of window "Notification Center" of application process "NotificationCenter" of application "System Events"
    
    -- 取得したグループ内のスクロールエリアの一番目のメニューボタンをクリック
    perform action 1 of menu button 1 of scroll area 1 of group 1 of targetGroup
    
    -- メニューが開いた後、最後のメニュー項目を選択（バナー以外の通知も削除する）
    perform action 3 of last menu item of menu 1 of targetGroup
end tell

```

## 動作

通知センターを開いた状態で上記のAppleScriptを実行すると以下のようにすべての通知が削除されます。

![screen-recording-66.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/56047138-67bc-48fb-b2b6-f3c477e7f8ff.gif)
