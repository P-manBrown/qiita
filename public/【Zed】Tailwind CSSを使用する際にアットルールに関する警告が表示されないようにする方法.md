---
title: 【Zed】Tailwind CSSを使用する際にアットルールに関する警告が表示されないようにする方法
tags:
  - tailwindcss
  - ZedEditor
private: false
updated_at: '2026-03-14T20:11:14+09:00'
id: 4728e800103fc7f49243
organization_url_name: null
slide: false
ignorePublish: false
---

## はじめに

ZedでTailwind CSSを使っていると、CSSファイル内に書いた `@apply` や `@layer`、`@theme` などのアットルールに対して警告（Unknown at rule）が表示されることがあります。

これはZedのデフォルトのCSSランゲージサーバー（`vscode-css-language-server`）がTailwind独自の構文を認識しないために起きます。

この記事では、Tailwind CSS専用のランゲージサーバーに切り替えることで警告を解消する方法を紹介します。

## 環境

- Zed（最新版推奨）
- Tailwind CSS v3 / v4

## 問題の再現

たとえば以下のようなCSSファイルを書いたとき、`@apply` や `@layer` に対して警告が表示されます。

```css
@layer base {
  h1 {
    @apply text-2xl font-bold;
  }
}

@layer utilities {
  .text-balance {
    text-wrap: balance;
  }
}
```

デフォルトのCSSランゲージサーバーはTailwindのアットルールを知らないため、`Unknown at rule` などの警告を出してしまいます。

## 解決方法

ZedのCSSファイルに対するランゲージサーバーを `tailwindcss-intellisense-css` に切り替えます。

このランゲージサーバーは、通常のCSS IntelliSense機能（補完・ホバー・定義ジャンプなど）を維持しつつ、Tailwind独自のアットルールも正しく認識します。

### 設定手順

`cmd + ,` でSettings（`settings.json`）を開き、以下の設定を追加します。

```json
{
  "languages": {
    "CSS": {
      "language_servers": [
        "tailwindcss-intellisense-css",
        "!vscode-css-language-server",
        "..."
      ]
    }
  }
}
```

各行の意味は次のとおりです。

- `"tailwindcss-intellisense-css"` ： Tailwind対応のCSSランゲージサーバーを有効化する
- `"!vscode-css-language-server"` ： デフォルトのCSSランゲージサーバーを無効化する（先頭の `!` が無効化の意味）

設定後はZedを再起動するか、ファイルを開き直すと反映されます。

## 設定後の動作

設定後は `@apply`、`@layer`、`@theme` などのアットルールが正しく認識され、警告が表示されなくなります。

また、通常のCSS補完やホバープレビューも引き続き機能するため、開発体験が損なわれることはありません。

```css
/* 設定後は警告なしで書ける */
@theme {
  --color-primary: oklch(0.6 0.15 240);
}

@layer components {
  .btn {
    @apply px-4 py-2 rounded-lg font-medium;
  }
}
```

## 参考

https://zed.dev/docs/languages/tailwindcss#using-tailwind-css-mode-in-css-files
