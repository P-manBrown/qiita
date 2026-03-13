---
title: 【Ghostty】v1.3の新機能
tags:
  - ghostty
private: false
updated_at: '2026-03-13T20:07:04+09:00'
id: 57dc921401bf420c055a
organization_url_name: null
slide: false
ignorePublish: false
---
## スクロールバック検索

ターミナルの履歴全体を検索できる機能が追加されました。

- **Mac**: `Cmd+F`
- **Linux**: `Ctrl+Shift+F`

検索バーは画面の四隅にドラッグして移動可能です。

## ネイティブスクロールバー

すべてのプラットフォームで、OSネイティブのスクロールバーが利用できるようになりました。

```toml
scrollbar = always   # 常に表示
scrollbar = never    # 常に非表示
scrollbar = auto     # 自動（デフォルト）
```

## クリックでカーソル移動

**Fish v4以上**と**Nushell v0.11以上**では、シェルプロンプト内をクリックしてカーソルを移動できます。

## プロセス完了時の通知

長時間実行されたコマンド完了時にプッシュ通知を受け取れます。

```toml
notify-on-command-finish = unfocused
notify-on-command-finish-action = no-bell,notify
notify-on-command-finish-after = 30s
```

## リッチテキスト形式でのコピー

テキストをコピーする際に、ターミナルの**色やフォーマット属性が保持**されるようになりました。Google DocsやWordなどにペーストすると色付けが維持されます。

## パフォーマンス向上

Claude Code使用時のメモリリークが修正され、大規模データ処理が大幅に高速化されました。

## macOS専用機能

### AppleScript対応

AppleScriptでターミナル操作を自動化できます（プレビュー機能）。

```applescript
tell application "Ghostty"
    set term to focused terminal of selected tab of front window
    input text "pwd\n" to term
end tell
```

### スプリットのドラッグ&ドロップ

スプリット上部のハンドルをドラッグして、任意の位置に移動できます。

## 参考

https://ghostty.org/docs/install/release-notes/1-3-0
