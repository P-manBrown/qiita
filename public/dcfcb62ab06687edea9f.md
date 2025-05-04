---
title: 【VSCode】Solargraphの導入【Ruby】
tags:
  - Ruby
  - Rails
  - VSCode
  - solargraph
private: false
updated_at: '2022-07-13T03:49:30+09:00'
id: dcfcb62ab06687edea9f
organization_url_name: null
slide: false
ignorePublish: false
---
## 拡張機能をインストールする
solargaphの拡張機能をVSCodeにインストールします。

https://marketplace.visualstudio.com/items?itemName=castwide.solargraph

## gemをインストールする
solargraphをグローバルインストールする場合には以下のとおりインストールします。

```:ターミナル
$ gem install solargraph

# グローバルなgemのdocumentを生成。
$ yard gems
```
`bundle exec`しないように`settings.json`に以下のように記述します。

```settings.json
"solargraph.useBundler": false
```

bundlerでinstallする場合には以下のとおりインストールします。

```:Gemfile
group :development do
  gem "solargraph"
end
```

```bash
$ bundle install

# プロジェクトにインストールしているgemのdocumentを生成
$ bundle exec yard gems
```

`bundle exec`しないように`settings.json`は以下のように記述します。

```setting.json
"solargraph.useBundler": true
```

また、`rubocop`を使用してファイル保存時にフォーマットしたい場合には以下のように記述します。
`solargraph.useBundler`はインストール方法に合わせて変更してください。

```setting.json
{ 
  "editor.defaultFormatter": "castwide.solargraph",
  "solargraph.useBundler": true, 
  "solargraph.diagnostics": true,
  "solargraph.formatting": true,
}

```

## 設定ファイルを作成

以下のコマンドを実行してsolargraphの設定ファイルを作成します。
```:ターミナル
$ solargraph config .
```
設定の詳細については以下のページをご参照ください。

https://solargraph.org/guides/configuration


