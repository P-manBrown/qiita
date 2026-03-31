---
title: 【Zed】ホットキーでダークテーマとライトテーマを切り替える方法
tags:
  - ZedEditor
private: false
updated_at: '2026-03-31T23:46:39+09:00'
id: b0a85bae976eff25afad
organization_url_name: null
slide: false
ignorePublish: false
---

## デフォルトのホットキー

| OS | ショートカット |
|---|---|
| macOS | `Cmd+K` → `Cmd+Shift+T` |
| Linux / Windows | `Ctrl+K` → `Ctrl+Shift+T` |

コマンドパレット（`Cmd+Shift+P` / `Ctrl+Shift+P`）で `theme: toggle mode` と検索しても同じアクションを実行できます。

## 切り替えの動作

ホットキーを押すたびに、テーマのモードが **ライト → ダーク → ライト** と交互に切り替わります。

現在のモードが「システム連動（system）」の場合は、システムの現在の外観を基準にして逆のモードへ切り替わります。

## 静的テーマ（Static）から動的テーマ（Dynamic）への自動移行

`settings.json` で以下のようにテーマを単一で指定している場合（静的モード）、

```json
{
  "theme": "Any Theme"
}
```

**初回のトグル時に自動で動的モードへ変換**されます。変換後の設定は次のようになります。

```json
{
  "theme": {
    "mode": "system",
    "light": "One Light",
    "dark": "One Dark"
  }
}
```

`light` と `dark` にはデフォルトテーマが設定されます。自分好みのテーマに変更したい場合は、初回トグル後に手動で書き換えてください。

なお、`light` と `dark` に同じテーマが設定されている状態でトグルしても、見た目の変化がわかりにくい場合があります。異なるテーマを設定しておくことをおすすめします。

## 動的モードでの設定例

ライト／ダーク用のテーマをあらかじめ設定しておきたい場合は、`settings.json` を以下のように記述します。

```json
{
  "theme": {
    "mode": "dark",
    "light": "One Light",
    "dark": "One Dark"
  }
}
```

`mode` を `"light"` または `"dark"` にしておくと、ホットキーで切り替えたときにそれぞれのテーマが適用されます。

## ホットキーのカスタマイズ

デフォルトのホットキーを変更したい場合は、`keymap.json`（`Cmd+K Cmd+S` / `Ctrl+K Ctrl+S` で開く）に以下を追記します。

```json
[
  {
    "context": "Workspace",
    "bindings": {
      "ctrl-shift-l": "theme::ToggleMode"
    }
  }
]
```

`"ctrl-shift-l"` の部分は任意のキーに変更してください。

## 参考

https://github.com/zed-industries/zed/pull/49027
