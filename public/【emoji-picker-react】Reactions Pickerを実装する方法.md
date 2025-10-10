---
title: 【emoji-picker-react】Reactions Pickerを実装する方法
tags:
  - 'emoji-picker-react'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 実装方法

Reactions Pickerを使用するには、`reactionsDefaultOpen`プロップを`true`に設定します。

```jsx
import Picker from 'emoji-picker-react';

function App() {
  const handleReaction = (emojiData) => {
    console.log('Selected emoji:', emojiData);
  };

  return (
    <Picker 
      reactionsDefaultOpen={true}
      onReactionClick={handleReaction}
    />
  );
}
```

## Reactions Pickerのカスタマイズ

表示するReactions Pickerに表示される絵文字をカスタマイズするには、`reactions`プロップにunified emoji IDの配列を渡します。

```jsx
<Picker 
  reactionsDefaultOpen={true}
  onReactionClick={handleReaction}
  reactions={['1f44d', '2764-fe0f', '1f389', '1f440', '1f914']}
/>
```

この例では、👍❤️🎉👀🤔 の5つの絵文字がリアクションとして表示されます。

## 参考

https://github.com/ealush/emoji-picker-react/blob/master/README.md#reactions-picker
