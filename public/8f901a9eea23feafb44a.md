---
title: 【Mac】ターミナルでリマインダーの一覧を表示する方法
tags:
  - Mac
private: false
updated_at: '2023-08-20T00:01:01+09:00'
id: 8f901a9eea23feafb44a
organization_url_name: null
slide: false
ignorePublish: false
---

## AppleScriptで取得する

次のコマンドを実行することでリマインダーの一覧を取得できます。

```terminal
osascript -e 'tell application "Reminders" to get name of every reminder' | tr ',' '\n'
```

```terminal
$ osascript -e 'tell application "Reminders" to get name of every reminder' | tr ',' '\n'
タスク1
タスク2
タスク3
タスク4
```

未完了のタスクのみ取得する場合には次のコマンドを実行します。

```terminal
osascript -e 'tell application "Reminders" to get name of every reminder whose completed is false' | tr ',' '\n'
```

```terminal
$ osascript -e 'tell application "Reminders" to get name of every reminder whose completed is false' | tr ',' '\n'
未完了タスク1
未完了タスク2
未完了タスク3
```

## reminders-cliで取得する

reminders-cliをインストールします。

```terminal
brew install keith/formulae/reminders-cli
```

次のコマンドを実行して特定のリストのリマインダー一覧を取得します。

```terminal
$ reminders show リスト名
0 タスク1
1 タスク2
2 タスク3
```
