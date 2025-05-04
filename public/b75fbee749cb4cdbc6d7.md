---
title: 【HTML】inert属性について
tags:
  - HTML
private: false
updated_at: '2024-10-19T23:55:08+09:00'
id: b75fbee749cb4cdbc6d7
organization_url_name: null
slide: false
ignorePublish: false
---
## `inert`属性とは

`inert`属性は、HTMLの要素に対して適用される属性で、要素を「無効化」するために使用されます。この属性が設定された要素は、ユーザーインターフェースの一部としては存在しますが、ユーザーがその要素に対して操作を行うことができなくなります。具体的には、以下のことをします。

- ユーザーが要素をクリックしたときにclickイベントが発生するのを防ぎます
- 要素にフォーカスが当たらないようにすることで、focusイベントが発生するのを防ぎます
- ブラウザのページ内検索機能の使用中に、要素の内容が検索/マッチされるのを防ぎます
- ユーザーが要素内のテキストを選択できないようにします（CSSプロパティのuser-selectを使用してテキストの選択を無効にするのと同じです）
- ユーザが要素の内容を編集できないようにします
- アクセシビリティ・ツリーから除外することで、要素やその内容を支援技術から隠します

## 使用例

以下は、`inert`属性を使用した簡単な例です。

```html
<div id="container" inert>
    <button>ボタン1</button>
    <button>ボタン2</button>
</div>

<button id="toggle">無効化の切り替え</button>

<script>
    const toggleButton = document.getElementById('toggle');
    const container = document.getElementById('container');

    toggleButton.addEventListener('click', () => {
        container.toggleAttribute('inert');
    });
</script>
```

この例では、`container`という`div`要素に`inert`属性が設定されており、「ボタン1」と「ボタン2」はクリックなどの操作ができなくなっています。
`toggle`ボタンをクリックし、`inert`属性を切り替えると「ボタン1」と「ボタン2」をクリックできるようになります。

## 参考

https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/inert
