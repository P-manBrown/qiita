---
title: 【Mac】ターミナルでアプリケーションの起動や終了をする方法
tags:
  - ShellScript
  - Mac
  - AppleScript
private: false
updated_at: '2023-06-07T02:24:16+09:00'
id: 9acb4dc36d0f9fd5b60d
organization_url_name: null
slide: false
ignorePublish: false
---
## アプリケーションを起動する
アプリケーションを起動するには次のようにコマンドを実行します。

```terminal
osascript -e 'tell application "アプリケーション名" to run'
```

以下のコマンドを実行するとリマインダーが起動します。

```terminal
osascript -e 'tell application "Reminders" to run'
```

次のように実行してもアプリケーションを起動できます。
こちらの場合には上記と違い、ウィンドウも表示されます。

```terminal
osascript -e 'tell application "アプリケーション名" to activate'
```

以下のコマンドを実行するとリマインダーが起動し、ウィンドウが表示されます。

```terminal
osascript -e 'tell application "Reminders" to activate'
```

また、次のコマンドも`activate`と同様の結果になります。

```terminal
open -a 'アプリケーション名.app'
```

## アプリケーションを終了する
アプリケーションを起動するには次のようにコマンドを実行します。


```terminal
osascript -e 'tell application "アプリケーション名" to quit'
```

以下のコマンドを実行するとリマインダーが終了します。

```terminal
osascript -e 'tell application "Reminders" to quit'
```
