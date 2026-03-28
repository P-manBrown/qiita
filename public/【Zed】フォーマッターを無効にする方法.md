---
title: 【Zed】フォーマッターを無効にする方法
tags:
  - ZedEditor
private: false
updated_at: '2026-03-28T23:55:24+09:00'
id: 42c2ee474f4b72eefbc7
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Zedエディタでは、保存時に自動でコードを整形してくれる**フォーマッター**機能が搭載されています。しかし、プロジェクトによってはフォーマッターを使いたくない場面もあります。

- 既存のコードスタイルを崩したくない
- フォーマット処理でエディタが重くなるのを防ぎたい
- フォーマッターはCIに任せてエディタ側では動かしたくない
- `code_actions_on_format`（保存時のコードアクション）だけを有効にしたい

これまでは `"formatter": null` を設定してもフォーマッターを完全に無効化することはできませんでした。`null` は設定を未定義と同等に扱うため、結局デフォルト動作（`"auto"` または言語サーバーによるフォーマット）にフォールバックしていたためです。

2026年3月17日にマージされたPR #48991により、`"formatter": "none"` という新しいオプションが追加され、フォーマッターを明示的に無効化できるようになりました。



## 設定方法

### グローバルに無効化する

エディタ全体でフォーマッターを無効にするには、`settings.json` に以下を追記します。

```json
{
  "formatter": "none"
}
```

`Cmd + Shift + P`（macOS）でコマンドパレットを開き、`open settings` と入力すると設定ファイルを編集できます。

### 特定の言語のみ無効化する

言語ごとに設定を上書きすることも可能です。たとえばJavaScriptだけフォーマッターを無効にしたい場合は次のように書きます。

```json
{
  "languages": {
    "JavaScript": {
      "formatter": "none"
    }
  }
}
```

TypeScriptとJavaScriptの両方を対象にする場合は、それぞれ指定します。

```json
{
  "languages": {
    "JavaScript": {
      "formatter": "none"
    },
    "TypeScript": {
      "formatter": "none"
    }
  }
}
```

### プロジェクト単位で無効化する

プロジェクトルートに `.zed/settings.json` を作成することで、そのプロジェクトだけに設定を適用できます。

```json
{
  "formatter": "none"
}
```

チームメンバー全員に同じ設定を共有したい場合や、プロジェクトごとに異なるフォーマット方針を持たせたい場合に便利です。

## `null` との違い

以前から `"formatter": null` という書き方は可能でしたが、動作が異なります。

| 設定値 | 動作 |
|---|---|
| `"formatter": null` | 未定義と同等。`"auto"` や言語サーバーにフォールバックする |
| `"formatter": "none"` | フォーマッターを完全に無効化する |

`null` はあくまで「設定を指定しない」という意味であるのに対し、`"none"` は「明示的に無効にする」という意図を持つ値です。

## `code_actions_on_format` は引き続き動作する

`"formatter": "none"` はフォーマット処理のみを無効にします。`code_actions_on_format` に設定したコードアクション（例：保存時に `organize imports` を実行するなど）は引き続き機能します。

```json
{
  "formatter": "none",
  "code_actions_on_format": {
    "source.organizeImports": true
  }
}
```

フォーマットはしたくないけれど、インポートの整理だけは自動化したい、といったユースケースで活用できます。

## 参考

https://github.com/zed-industries/zed/pull/48991
