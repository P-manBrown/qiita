---
title: 【React】カスタムフックにイベントハンドラーを渡す方法
tags:
  - React
private: false
updated_at: '2026-02-23T22:19:00+09:00'
id: 030dfb919d99aee23e56
organization_url_name: null
slide: false
ignorePublish: false
---
## 実装方法

`onReceiveMessage` をオプションとして受け取るようにします。
以下のように`useEffectEvent` を使うと、イベントハンドラーを依存配列から除外できます。
コンポーネントが再レンダリングされても不必要な再接続が発生しなくなります。

```js
import { useEffect, useEffectEvent } from 'react';

export function useChatRoom({ serverUrl, roomId, onReceiveMessage }) {
  // イベントハンドラーを Effect Event としてラップ
  const onMessage = useEffectEvent(onReceiveMessage);

  useEffect(() => {
    const connection = createConnection({ serverUrl, roomId });
    connection.connect();
    connection.on('message', (msg) => {
      onMessage(msg); // 依存配列に含めなくてOK
    });
    return () => connection.disconnect();
  }, [roomId, serverUrl]); // ✅ onMessage は依存配列に不要
}
```

以下の実装では `onReceiveMessage` を依存配列に追加しているため、コンポーネントが再レンダリングされるたびに関数の参照が変わり、Effectが再実行されてしまいます（＝チャットが再接続される）。

```js
// useChatRoom.js
export function useChatRoom({ serverUrl, roomId, onReceiveMessage }) {
  useEffect(() => {
    const connection = createConnection({ serverUrl, roomId });
    connection.connect();
    connection.on('message', (msg) => {
      onReceiveMessage(msg); // コンポーネントから渡された処理を呼ぶ
    });
    return () => connection.disconnect();
  }, [roomId, serverUrl, onReceiveMessage]); // onReceiveMessage を依存配列に追加
}
```

## 参考

https://react.dev/learn/reusing-logic-with-custom-hooks#passing-event-handlers-to-custom-hooks
