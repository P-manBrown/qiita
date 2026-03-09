---
title: 【Mac】ステージマネージャをターミナルから操作する方法
tags:
  - macOS
  - Stage Manager
  - ターミナル
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 基本コマンド

ステージマネージャの設定は `com.apple.WindowManager` ドメインの `defaults` コマンドで管理されています。

### 有効化する

```bash
defaults write com.apple.WindowManager GloballyEnabled -bool true
```

### 無効化する

```bash
defaults write com.apple.WindowManager GloballyEnabled -bool false
```

### 現在の状態を確認する

```bash
defaults read com.apple.WindowManager GloballyEnabled
```

`1` が返れば有効、`0` が返れば無効です。

:::note info
設定変更はすぐに反映されます。`killall` などのプロセス再起動は不要です。
:::

## その他の設定項目

`com.apple.WindowManager` ドメインには他にも設定項目があります。

### 最近使ったアプリのサムネイルを自動非表示にする

```bash
# 自動非表示 ON（左端にカーソルを持っていくと表示）
defaults write com.apple.WindowManager AutoHide -bool true

# 自動非表示 OFF（常に表示）
defaults write com.apple.WindowManager AutoHide -bool false
```

### アプリのウィンドウ表示方法

```bash
# 一度にすべてのウィンドウを表示（All at Once）
defaults write com.apple.WindowManager AppWindowGroupingBehavior -bool false

# 1枚ずつ表示（One at a Time）
defaults write com.apple.WindowManager AppWindowGroupingBehavior -bool true
```

### デスクトップクリックの挙動（macOS Sonoma 以降）

```bash
# クリックで常にデスクトップを表示
defaults write com.apple.WindowManager EnableStandardClickToShowDesktop -bool true

# ステージマネージャ使用時のみデスクトップを表示
defaults write com.apple.WindowManager EnableStandardClickToShowDesktop -bool false
```

## まとめ

| 操作 | コマンド |
|------|---------|
| 有効化 | `defaults write com.apple.WindowManager GloballyEnabled -bool true` |
| 無効化 | `defaults write com.apple.WindowManager GloballyEnabled -bool false` |
| 状態確認 | `defaults read com.apple.WindowManager GloballyEnabled` |
| 設定リセット | `defaults delete com.apple.WindowManager && killall WindowManager` |

ターミナルから操作できると、Keyboard Maestro のマクロや Shell Script と組み合わせてショートカットキーで瞬時に切り替えるといった自動化も簡単に実現できます。

## 参考

https://support.apple.com/guide/mac-help/use-stage-manager-mchl534ba392/mac

https://www.hexnode.com/mobile-device-management/help/script-to-enable-disable-stage-manager-on-mac/

https://forum.keyboardmaestro.com/t/how-to-detect-stage-manager-state/34802

https://apple.stackexchange.com/questions/453963/terminal-command-to-enable-disable-stage-manager-in-the-new-system-settings-in
