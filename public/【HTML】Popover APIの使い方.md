---
title: 【HTML】Popover APIの使い方
tags:
  - HTML
  - JavaScript
  - フロントエンド
  - アクセシビリティ
  - UI開発
private: false
updated_at: '2026-03-08T23:39:13+09:00'
id: 02ab948d289249e335cb
organization_url_name: null
slide: false
ignorePublish: false
---

## はじめに

ツールチップやポップアップを実装しようとして、JavaScriptのイベントリスナーを何行も書いた経験はありませんか？  
**Popover API** を使えば、そのような実装の多くをHTMLだけで宣言的に記述できます。

この記事では、Popover APIの基本から応用まで、コード例を交えて解説します。

## Popover APIとは？

Popover APIは、ツールチップ・ポップオーバー・コンテキストメニューなどの「オーバーレイUI」をネイティブのHTMLで実現するための仕組みです。

従来はこれらを作るために：
- JavaScriptでの開閉管理
- `aria-expanded` などのARIA属性の手動更新
- `Esc`キーの処理
- フォーカス管理

これらをすべて自前で実装する必要がありました。Popover APIはその多くをブラウザが肩代わりしてくれます。

### ブラウザサポート

2024年以降、Chrome・Firefox・Safari・Edgeすべての主要ブラウザで利用可能です。最新の対応状況は [Caniuse](https://caniuse.com/?search=popover+api) で確認してください。

## 基本的な使い方

### `popover` 属性と `popovertarget` 属性

最小限の実装はこれだけです。

```html
<button popovertarget="my-popover">ポップオーバーを開く</button>

<div id="my-popover" popover>
  これがポップオーバーのコンテンツです。
</div>
```

- `popovertarget="id"` ：ボタンとポップオーバー要素を紐付ける
- `popover` 属性：この要素がポップオーバーであることをブラウザに伝える

**JavaScriptは一切不要です。** ボタンをクリックするとポップオーバーが開き、`Esc`キーを押すか外側をクリックすると閉じます。

### `popovertargetaction` 属性

ボタンの動作を細かく制御できます。

```html
<!-- 開くボタン -->
<button popovertarget="my-popover" popovertargetaction="show">開く</button>

<!-- 閉じるボタン -->
<button popovertarget="my-popover" popovertargetaction="hide">閉じる</button>

<!-- 開閉トグル（デフォルト） -->
<button popovertarget="my-popover" popovertargetaction="toggle">トグル</button>

<div id="my-popover" popover>
  コンテンツ
</div>
```

| 値 | 動作 |
|---|---|
| `show` | ポップオーバーを開く |
| `hide` | ポップオーバーを閉じる |
| `toggle` | 開閉を切り替える（デフォルト） |

## 表示モード：`auto` と `manual`

`popover` 属性には2種類のモードがあります。

### `popover="auto"` （デフォルト）

```html
<button popovertarget="auto-popover">開く</button>

<div id="auto-popover" popover="auto">
  <p>外側をクリックすると閉じます（light dismiss）</p>
</div>
```

**特徴：**
- 外側をクリックすると自動で閉じる（**light dismiss**）
- `Esc`キーで閉じる
- 同時に複数の `auto` ポップオーバーは開けない（新しく開くと前のが閉じる）
- `popover` 属性のみの指定は `popover="auto"` と同じ意味

### `popover="manual"`

```html
<button popovertarget="manual-popover" popovertargetaction="show">開く</button>
<button popovertarget="manual-popover" popovertargetaction="hide">閉じる</button>

<div id="manual-popover" popover="manual">
  <p>明示的に閉じる操作が必要です</p>
</div>
```

**特徴：**
- 外側をクリックしても閉じない
- `Esc`キーでも自動では閉じない
- 閉じる処理を完全に自前で制御したい場合に使用
- 複数同時に開くことが可能

### どちらを使うべき？

| ユースケース | 推奨モード |
|---|---|
| ツールチップ | `manual` |
| ドロップダウンメニュー | `auto` |
| 通知バナー | `manual` |
| コンテキストメニュー | `auto` |
| モーダル的な案内 | `auto` |

## JavaScriptからの操作

JavaScriptから制御することも可能です。

```javascript
const popover = document.getElementById('my-popover');

// 開く
popover.showPopover();

// 閉じる
popover.hidePopover();

// トグル
popover.togglePopover();
```

### イベントの検知

```javascript
const popover = document.getElementById('my-popover');

popover.addEventListener('beforetoggle', (event) => {
  console.log(`${event.oldState} → ${event.newState}`);
  // 例: "closed → open" または "open → closed"
});

popover.addEventListener('toggle', (event) => {
  if (event.newState === 'open') {
    console.log('ポップオーバーが開きました');
  } else {
    console.log('ポップオーバーが閉じました');
  }
});
```

## 具体的なUIパターンへの応用

### 1. ツールチップ

```html
<button popovertarget="help-tip" popovertargetaction="show" aria-describedby="help-tip">
  ？
</button>

<div id="help-tip" popover="manual" role="tooltip">
  ここをクリックするとヘルプが表示されます。
</div>
```

ホバー時の遅延など、より自然な挙動が必要な場合は少量のJavaScriptを追加します。

```javascript
const trigger = document.querySelector('[popovertarget="help-tip"]');
const tooltip = document.getElementById('help-tip');
let hideTimeout;

trigger.addEventListener('mouseenter', () => {
  clearTimeout(hideTimeout);
  tooltip.showPopover();
});

trigger.addEventListener('mouseleave', () => {
  hideTimeout = setTimeout(() => tooltip.hidePopover(), 200);
});

tooltip.addEventListener('mouseenter', () => clearTimeout(hideTimeout));
tooltip.addEventListener('mouseleave', () => {
  hideTimeout = setTimeout(() => tooltip.hidePopover(), 200);
});
```

### 2. ドロップダウンメニュー

```html
<button popovertarget="dropdown-menu">
  メニュー ▼
</button>

<ul id="dropdown-menu" popover="auto" role="menu">
  <li role="menuitem"><a href="/profile">プロフィール</a></li>
  <li role="menuitem"><a href="/settings">設定</a></li>
  <li role="menuitem"><a href="/logout">ログアウト</a></li>
</ul>
```

```css
#dropdown-menu {
  margin: 0;
  padding: 8px 0;
  list-style: none;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

#dropdown-menu li a {
  display: block;
  padding: 8px 16px;
  text-decoration: none;
  color: #333;
}

#dropdown-menu li a:hover {
  background-color: #f5f5f5;
}
```

### 3. 通知バナー（自動クローズ）

```html
<div id="notification" popover="manual" role="status" aria-live="polite">
  ✅ 保存しました！
</div>
```

```javascript
const notification = document.getElementById('notification');

function showNotification(message) {
  notification.textContent = message;
  notification.showPopover();

  // 3秒後に自動で閉じる
  setTimeout(() => {
    notification.hidePopover();
  }, 3000);
}

// 使用例
document.getElementById('save-btn').addEventListener('click', () => {
  showNotification('✅ 保存しました！');
});
```

### 4. コンテキストメニュー（右クリックメニュー）

```html
<div id="context-area">右クリックしてください</div>

<menu id="context-menu" popover="auto">
  <li><button>コピー</button></li>
  <li><button>貼り付け</button></li>
  <li><button>削除</button></li>
</menu>
```

```javascript
const contextArea = document.getElementById('context-area');
const contextMenu = document.getElementById('context-menu');

contextArea.addEventListener('contextmenu', (event) => {
  event.preventDefault();

  // メニューを表示位置に移動
  contextMenu.style.left = `${event.clientX}px`;
  contextMenu.style.top = `${event.clientY}px`;

  contextMenu.showPopover();
});
```

## CSSでのスタイリング

### `:popover-open` 疑似クラス

ポップオーバーが開いているときだけスタイルを適用できます。

```css
[popover] {
  /* デフォルトスタイルのリセット */
  border: none;
  padding: 12px 16px;
  border-radius: 8px;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.2);
}

[popover]:popover-open {
  /* 開いているときのスタイル */
  display: block;
}
```

### アニメーション

`@starting-style` を使ってフェードインアニメーションを実装できます。

```css
[popover] {
  opacity: 0;
  transform: translateY(-8px);
  transition: opacity 0.2s ease, transform 0.2s ease,
              display 0.2s ease allow-discrete,
              overlay 0.2s ease allow-discrete;
}

[popover]:popover-open {
  opacity: 1;
  transform: translateY(0);
}

@starting-style {
  [popover]:popover-open {
    opacity: 0;
    transform: translateY(-8px);
  }
}
```

## アクセシビリティへの配慮

Popover APIはアクセシビリティの多くをブラウザが自動的に処理してくれますが、正しく使うためのポイントを押さえておきましょう。

### 自動で行われること

- `Esc`キーによる閉じる動作
- `aria-expanded` 属性の自動更新
- フォーカスの適切な管理（`auto`モードの場合）

### 開発者が設定すべきこと

**`role` 属性を適切に指定する**

```html
<!-- ツールチップの場合 -->
<div id="tip" popover="manual" role="tooltip">説明文</div>

<!-- ダイアログ的な場合 -->
<div id="dialog" popover="auto" role="dialog" aria-labelledby="dialog-title">
  <h2 id="dialog-title">タイトル</h2>
  <p>コンテンツ</p>
</div>

<!-- ステータス通知の場合 -->
<div id="notice" popover="manual" role="status" aria-live="polite">
  処理が完了しました
</div>
```

**トリガー要素との関連付け**

```html
<button
  popovertarget="help-tip"
  aria-describedby="help-tip">
  ヘルプ
</button>

<div id="help-tip" popover="manual" role="tooltip">
  詳しい説明はこちら
</div>
```

**キーボード操作のチェックリスト**
- `Tab` / `Shift+Tab` でフォーカスが正しく移動するか
- `Esc` キーでポップオーバーが閉じるか（`auto`モードは自動）
- フォーカスがポップオーバーを閉じた後に適切な位置に戻るか

## `<dialog>` との使い分け

Popover APIと似た要素に `<dialog>` があります。使い分けの目安を整理します。

| 特徴 | Popover API | `<dialog>` |
|---|---|---|
| フォーカストラップ | なし | あり（モーダル時） |
| 背景スクロール | 可能 | ブロック（モーダル時） |
| ページ上のコンテキスト維持 | ◎ | △ |
| 向いているUI | ツールチップ、メニュー、通知 | 確認ダイアログ、フォーム |
| light dismiss | `auto`モードで可能 | `showModal()`では不可 |

**基本方針**
- ユーザーがページのコンテキストを維持したまま使える → **Popover API**
- 必ずユーザーの応答が必要（「削除しますか？」など）→ **`<dialog>`**

## まとめ

Popover APIを使うことで、これまでJavaScriptで実装していた多くのUI挙動をHTMLだけで宣言的に記述できます。

**Popover APIのメリット**
- `Esc`キー・light dismissなどの挙動をブラウザが処理
- ARIA属性の自動更新でアクセシビリティを確保
- コード量の大幅削減
- メンテナンスコストの低下

**適切に使い分けるポイント**
- `popover="auto"` → 外側クリックで閉じる、シンプルなUI向け
- `popover="manual"` → 閉じるタイミングを自分で制御したいとき
- 複雑なポジショニングが必要な場合はCSS Anchor Positioningや専用ライブラリを検討

まずは既存のツールチップを1つだけPopover APIで書き直してみてください。どれだけコードが減るか、体感できるはずです。

## 参考

https://developer.mozilla.org/ja/docs/Web/API/Popover_API

https://html.spec.whatwg.org/multipage/popover.html#the-popover-attribute

https://www.smashingmagazine.com/2026/03/getting-started-popover-api/

https://open-ui.org/components/popover.research.explainer/

https://caniuse.com/?search=popover+api
