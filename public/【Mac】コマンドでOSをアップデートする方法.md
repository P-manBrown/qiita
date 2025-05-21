---
title: 【Mac】コマンドでOSをアップデートする方法
tags:
  - 'Mac'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

`softwareupdate`コマンドを使用してmacOSをアップデートできます。

## 利用可能なアップデートの一覧を取得

以下のコマンドを実行すると利用可能なアップデートの一覧が出力されます。

```terminal
softwareupdate -l
```

```terminal
$ softwareupdate -l

Software Update found the following new or updated software:
* Label: Command Line Tools for Xcode-15.3
	Title: Command Line Tools for Xcode, Version: 15.3, Size: 707501KiB, Recommended: YES, 
* Label: Command Line Tools beta 2 for Xcode-16.0
	Title: Command Line Tools beta 2 for Xcode, Version: 16.0, Size: 743581KiB, Recommended: YES
```

## 利用可能なすべてのアップデートをインストール

次のコマンドを実行すると利用可能なすべてのアップデートをインストールできます。

```terminal
sudo softwareupdate -i -a
```

## 特定のアップデートをインストール

アップデート名を指定すると特定のアップデートのみインストールできます。

```terminal
sudo softwareupdate -i "アップデート名"
```
