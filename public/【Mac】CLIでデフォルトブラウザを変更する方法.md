---
title: 【Mac】CLIでデフォルトブラウザを変更する方法
tags:
  - Mac
  - CLI
private: false
updated_at: '2026-05-12T22:16:45+09:00'
id: d481981f7a816c964a21
organization_url_name: null
slide: false
ignorePublish: false
---
## 方法1：`defaultbrowser` コマンドを使う（Safari・Firefox含む全ブラウザ対応）

`defaultbrowser` はHomebrewでインストールできるコマンドラインツールです。ChromiumベースではないSafariやFirefoxを含む、あらゆるブラウザに対応している点が特徴です。

### `defaultbrowser` のインストール

```bash
brew install defaultbrowser
```

### 使い方

インストール済みの利用可能なブラウザ一覧を確認するには、引数なしで実行します。

```bash
defaultbrowser
```

実行すると、以下のようにブラウザのリストが表示されます（インストール状況によって異なります）。

```
chrome
safari
firefox
brave
edge
```

ブラウザ名を引数に渡すと、そのブラウザがデフォルトに設定されます。

```bash
# Safariをデフォルトに設定
defaultbrowser safari

# Google Chromeをデフォルトに設定
defaultbrowser chrome

# Firefoxをデフォルトに設定
defaultbrowser firefox

# Braveをデフォルトに設定
defaultbrowser brave
```

コマンド実行後、macOSから「デフォルトブラウザの変更を許可しますか？」というダイアログが表示される場合があります。その場合は「使用する」をクリックして確定してください。

## 方法2：`open` コマンドのフラグを使う（Chromiumベースのブラウザ専用）

Google Chrome、Microsoft Edge、Brave といったChromiumベースのブラウザには、`--make-default-browser` という専用フラグが用意されています。Homebrewなどの追加ツールが不要なため、手軽に使えます。

```bash
# Google Chromeをデフォルトに設定
open -a "Google Chrome" --args --make-default-browser

# Microsoft Edgeをデフォルトに設定
open -a "Microsoft Edge" --args --make-default-browser

# Braveをデフォルトに設定
open -a "Brave Browser" --args --make-default-browser
```

`-a` オプションはアプリケーション名を指定し、`--args` 以降がそのアプリに渡される引数です。`--make-default-browser` はChromiumブラウザ固有のフラグなので、**SafariやFirefoxには使用できません**。

## 参考

https://osxdaily.com/2024/03/08/setting-the-default-web-browser-from-command-line-on-mac/
