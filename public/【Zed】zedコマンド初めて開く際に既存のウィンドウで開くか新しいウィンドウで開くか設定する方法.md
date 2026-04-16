---
title: 【Zed】zedコマンド初めて開く際に既存のウィンドウで開くか新しいウィンドウで開くか設定する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-04-17T00:09:15+09:00'
id: 3f861bef3828a9564109
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Zed v0.233.0（Preview）から、`zed <path>` コマンドを**初めて実行したとき**に、ファイルやディレクトリを既存のウィンドウで開くか、新しいウィンドウで開くかを選択するプロンプトが表示されるようになりました。

選択した内容は `cli_default_open_behavior` という設定として保存され、次回以降はプロンプトを表示せずにその挙動が使われます。

この記事では、この設定の概要と使い方を紹介します。

## 対象バージョン

- Zed v0.233.0（Preview）以降

## 設定の概要

`cli_default_open_behavior` は、`zed <path>` コマンドを実行したときの挙動を制御するトップレベルの設定です。

指定できる値は以下の2つです。

| 値 | 説明 |
|---|---|
| `"new_window"` | 毎回新しいウィンドウで開く |
| `"existing_window"` | 既存のウィンドウで開く |

## 初回実行時のプロンプト

設定が未指定の状態で `zed <path>` を実行すると、ターミナル上に「既存のウィンドウで開くか、新しいウィンドウで開くか」を選択するプロンプトが表示されます。

選択すると、その内容が `settings.json` に自動的に保存されます。

## 手動で設定する方法

プロンプトを経由せず、直接 `settings.json` に記述することもできます。

コマンドパレット（`Cmd+Shift+P` / `Ctrl+Shift+P`）から `zed: open settings` を実行して `settings.json` を開き、以下のように記述します。

### 新しいウィンドウで開く場合

```json
{
  "cli_default_open_behavior": "new_window"
}
```

### 既存のウィンドウで開く場合

```json
{
  "cli_default_open_behavior": "existing_window"
}
```

## CLIオプションとの使い分け

`cli_default_open_behavior` はあくまでデフォルトの挙動を決める設定です。コマンド実行時に個別のオプションを指定することで、設定に関係なく挙動を上書きすることができます。

- `zed -n <path>` … 常に新しいウィンドウで開く
- `zed -a <path>` … 現在フォーカスされているウィンドウにファイルを追加する

たとえばデフォルトを `"existing_window"` にしつつ、特定のプロジェクトだけ新しいウィンドウで開きたいときは `zed -n ./myproject` のように使い分けられます。

## 設定を変更したくなったとき

一度選択した設定を変更したい場合は、`settings.json` を直接編集して `cli_default_open_behavior` の値を書き換えるか、設定UIから検索して変更することができます。

コマンドパレットから `zed: open settings` を開き、`cli_default_open_behavior` を検索して値を変更してください。

## 参考

https://github.com/zed-industries/zed/pull/53663
