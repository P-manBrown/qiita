---
title: 【emoji-picker-react】CSS変数でピッカーのスタイルをカスタマイズする方法
tags:
  - emoji-picker-react
private: false
updated_at: '2025-10-22T21:52:52+09:00'
id: 66623755093492fc9442
organization_url_name: null
slide: false
ignorePublish: false
---
## カスタマイズ方法

### セレクターの指定

ピッカーのルートセレクターは `.EmojiPickerReact` です。カスタマイズする際は、より具体的なセレクターを使用する必要があります。

ダークモードの場合は `.EmojiPickerReact.epr-dark-theme` を使用します。


### 利用可能なCSS変数

以下のCSS変数を使用してスタイルをカスタマイズできます。

- `--epr-emoji-size`: 絵文字のサイズ
- `--epr-emoji-gap`: 絵文字間のスペース
- `--epr-hover-bg-color`: 絵文字ホバー時の背景色
- `--epr-bg-color`: ピッカーの背景色
  - この変数を変更する場合は、`--epr-category-label-bg-color` も同じ色に変更する必要があります
- `--epr-category-label-bg-color`: カテゴリラベルの背景色
- `--epr-text-color`: ピッカー内のテキスト色

## 実装例

```css
/* グローバルスタイルシート */
.custom-emoji-picker {
  --epr-bg-color: #ffffff;
  --epr-category-label-bg-color: #ffffff;
}

.custom-emoji-picker.epr-dark-theme {
  --epr-bg-color: #1a1a1a;
  --epr-category-label-bg-color: #1a1a1a;
}
```

```jsx
import EmojiPicker from 'emoji-picker-react';
import './styles.css';

function App() {
  return (
    <div className="custom-emoji-picker">
      <EmojiPicker />
    </div>
  );
}
```

## 参考

https://github.com/ealush/emoji-picker-react/blob/master/README.md#css-variables
