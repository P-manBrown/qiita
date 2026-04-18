---
title: 【Ghostty】スクロールバーを非表示にする方法
tags:
  - ghostty
private: false
updated_at: '2026-04-18T20:18:58+09:00'
id: f4ea93edd6a4015780eb
organization_url_name: null
slide: false
ignorePublish: false
---
## `scrollbar` オプションについて

Ghostty の設定ファイルには `scrollbar` というオプションがあり、スクロールバーの表示タイミングを制御できます。

指定できる値は以下の2つです。

**`system`（デフォルト）**
OS のシステム設定に従ってスクロールバーを表示します。macOS の場合、システム設定の「スクロールバーの表示」に応じて動作します。スクロール中やガター上にカーソルがある場合にのみ表示されるのが一般的です。

**`never`**
スクロールバーを常に非表示にします。マウスホイールやキーバインドによるスクロールは引き続き使用できます。

## 設定方法

Ghostty の設定ファイルを開きます。

```
~/.config/ghostty/config
```

以下の行を追加します。

```
scrollbar = never
```

設定を保存したあと、Ghostty を再起動するか、設定を再読み込みすると変更が反映されます。

## スクロールバーを表示に戻す場合

スクロールバーをシステム設定に戻したい場合は、以下のように変更します。

```
scrollbar = system
```

または該当行を削除しても同じ結果になります。デフォルト値が `system` のためです。

## 参考

https://ghostty.org/docs/config/reference#scrollbar
