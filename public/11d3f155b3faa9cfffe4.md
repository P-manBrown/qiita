---
title: 【Obsidian】テンプレートで前日や翌日の日付を入力する方法
tags:
  - Obsidian
private: false
updated_at: '2024-08-12T23:51:14+09:00'
id: 11d3f155b3faa9cfffe4
organization_url_name: null
slide: false
ignorePublish: false
---
## プラグインをインストールする

Templater というコミュニティプラグインをインストールし、有効化します。

https://github.com/SilentVoid13/Templater?tab=readme-ov-file

## テンプレートファイルを作成する

前日や翌日の日付を入力するには Templater の [tp.date](https://silentvoid13.github.io/Templater/internal-functions/internal-modules/date-module.html) を使用します。

```md:template.md
<<　[[<% tp.date.yesterday("YYYY-M-D") %> ]]　|　[[<% tp.date.tomorrow("YYYY-M-D") %>]]　>>
```

テンプレートを使用すると以下のように表示されます。

```md
<<　[[2024-8-11 ]]　|　[[2024-8-13]]　>>
```

デイリーノートコアプラグインなどでファイルを作成した際に動作させたい場合には設定の「Trigger Templater on new file creation」を有効にする必要があります。

![画像.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/c2ce71ab-1146-b6e9-0993-75a4233441c4.png)

