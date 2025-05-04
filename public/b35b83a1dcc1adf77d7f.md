---
title: 【Next.js】HTMLの構文チェックをする方法
tags:
  - HTML
  - Next.js
private: false
updated_at: '2024-12-04T23:55:07+09:00'
id: b35b83a1dcc1adf77d7f
organization_url_name: null
slide: false
ignorePublish: false
---
Markuplintを導入するとHTMLの構文チェックをすることができます。

https://markuplint.dev/ja/

## 導入のためのコマンドを実行する

以下のコマンドを実行し、

```terminal
$ yarn dlx markuplint --init
✔ Which do you use template engines? · React (JSX)
✔ May I install them automatically? (y/N) · true
✔ Do you customize rules? (y/N) · false
✔ Does it import the recommended config? (y/N) · true
```

`Which do you use template engines?` はカーソルを合わせ、スペースで選択します。

## 設定ファイルを編集する

上記のコマンドが完了すると `.markuplintrc` が生成されます。

```json:.markuplintrc
{
  "specs": {
    "\\.[jt]sx?$": "@markuplint/react-spec"
  },
  "parser": {
    "\\.[jt]sx?$": "@markuplint/jsx-parser"
  },
  "extends": [
    "markuplint:recommended"
  ]
}
```

`extends` を `markuplint:recommended` から `markuplint:recommende-react` に変更します。

次に `package.json` の `scripts` に `markuplint` を追加します。

```json:package.json
  "scripts": {
     "lint:jsx": "markuplint \"./**/*.tsx\"",
  },
```

以下のコマンドを実行し正常に動作するか確認します。

```terminal
yarn lint:jsx
```

## 参考

https://markuplint.dev/ja/docs/guides

https://markuplint.dev/ja/docs/guides/presets
