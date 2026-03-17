---
title: 【Zed】設定を簡単に切り替える方法
tags:
  - ZedEditor
private: false
updated_at: '2026-03-18T00:01:18+09:00'
id: 95eb073a66f6784ea755
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Zedには「設定プロファイル（Settings Profile）」という機能があり、あらかじめ定義した設定のセットをその場でスムーズに切り替えられます。

プレゼン用に文字サイズを大きくしたい、執筆モードに入りたい、テーマだけ変えたいといった場面で重宝する機能です。

この記事では、設定プロファイルの基本的な使い方と活用例を紹介します。

## 設定プロファイルとは

設定プロファイルとは、`settings.json` 内に定義する「設定の上書きセット」です。

プロファイルを選択すると、その中に記述した設定値が既存の設定に**上書き**される形で適用されます。プロファイルを解除すれば元の設定に戻ります。

## 設定方法

### 1. `settings.json` にプロファイルを定義する

コマンドパレット（`cmd+shift+p` / `ctrl+shift+p`）から `zed: open settings` を実行して `settings.json` を開き、`profiles` キーを追加します。

```json
{
  "profiles": {
    "Presenting (Dark)": {
      "buffer_font_size": 18.0,
      "ui_font_size": 18.0,
      "theme": "One Dark"
    },
    "Presenting (Light)": {
      "buffer_font_size": 18.0,
      "ui_font_size": 18.0,
      "theme": "One Light"
    },
    "Zen Writing": {
      "buffer_font_size": 16.0,
      "ui_font_size": 16.0,
      "theme": "Rosé Pine"
    }
  }
}
```

プロファイル名は自由に決められます。それぞれのプロファイルには、切り替えたい設定項目だけを書けばOKです。

### 2. プロファイルセレクターを開く

コマンドパレットから `settings profile selector: toggle` を実行します。

利用可能なプロファイルが一覧で表示されるので、選択するとその設定が即座に反映されます。

### 3. プロファイルを解除する

再度 `settings profile selector: toggle` を実行し、現在選択中のプロファイルを選ぶと解除されて元の設定に戻ります。


## 活用例

プロファイルには**ほぼすべての Zed 設定**を含めることができます。

**スクリーンショット・プレゼン用**

```json
"Presenting (Dark - Dracula)": {
  "buffer_font_size": 18.0,
  "agent_buffer_font_size": 18.0,
  "ui_font_size": 18.0,
  "theme": "Dracula"
}
```

**集中執筆モード**

```json
"Zen Writing": {
  "buffer_font_size": 16.0,
  "ui_font_size": 15.0,
  "theme": "Rosé Pine",
  "vim_mode": false,
  "show_whitespaces": "none"
}
```

**別の言語サーバーに切り替える**

```json
"Use Deno LSP": {
  "languages": {
    "TypeScript": {
      "language_servers": ["deno", "!typescript-language-server", "..."]
    }
  }
}
```

このように用途に合わせてプロファイルを定義しておけば、設定ファイルを直接編集することなくワンタッチで環境を切り替えられます。

## 参考

https://zed.dev/blog/hidden-gems-part-3#quick-swap-your-settings
