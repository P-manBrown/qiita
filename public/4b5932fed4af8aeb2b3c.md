---
title: 【JavaScript】リンクが新しいタブで開かれているか確認する方法
tags:
  - JavaScript
private: false
updated_at: '2023-09-11T23:56:41+09:00'
id: 4b5932fed4af8aeb2b3c
organization_url_name: null
slide: false
ignorePublish: false
---
以下のようにすることでリンクが新しいタブで開かれたか確認することができます。

```javascript
if (document.referrer) {
    if (history.length == 1) {
        console.log('リンクから新しいタブで開いた。')
    } else {
        console.log('リンクから同じウィンドウで開いた。');
    }
} else {
    console.log('アドレスバーにURLを入力して開いた。');
}
```
