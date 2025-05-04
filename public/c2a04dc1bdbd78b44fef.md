---
title: commit時にESlintとPrettierを実行する【ESLint】【Prettier】
tags:
  - ESLint
  - 初学者
  - prettier
  - lint-staged
  - husky
private: false
updated_at: '2022-07-09T03:00:54+09:00'
id: c2a04dc1bdbd78b44fef
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに
`git commit`をした際に`eslint --fix`と`prettier --write`を実行する方法について記載します。

### パッケージのインストール
以下のコマンドを実行して`husky`および`lint-staged`をインストールします。
```:ターミナル
$ yarn add -D husky lint-staged
```

### `lint-staged`の設定
lint-stagedの設定をします。
`package.json` に以下のように記述することでステージングしたファイルに対しコマンドを実行できます。
```package.json
  "lint-staged": {
    "*.{js,jsx,ts,tsx}": [
      "eslint --fix",
      "prettier --write"
    ]
  },
```

### `Git hooks`を有効化
以下コマンドを実行して`Git hooks`を有効化します。

```:ターミナル
yarn husky install
```

以下のように`.husky`ディレクトリが作成されます。
![スクリーンショット 2022-05-12 午前2.42.37.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/e805ff5f-3178-31a2-18d7-b33fa0f9e9b4.png)


`git clone`してパッケージをインストールした際に`Git hooks`を有効化するため、`package.json`に`prepare`を記述します。

yarn2以降を使用している場合には`prepare`は使用でないので`postinstall`を記述します。

```package.json
  "scripts": {
    "prepare": "husky install"
  },
```

```package.json
  "scripts": {
    "postinstall": "husky install"
  },
```


### `hooks`を作成
以下のコマンドを実行して`hooks`を作成します。
```:ターミナル
$ yarn husky add .husky/pre-commit "npx lint-staged"
```
実行すると`.husky`ディレクトリに`pre-commit`ファイルが作成されます。

![スクリーンショット 2022-05-12 午前2.50.15.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/e34af6af-0665-9086-f13b-15a5405e3811.png)


```pre-commit
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx lint-staged
```


### 確認
正常に動作する確認します。

```:ターミナル
$ git add .

$ git commit -m "test"
✔ Preparing lint-staged...
✔ Hiding unstaged changes to partially staged files...
✔ Running tasks for staged files...
✔ Applying modifications from tasks...
✔ Restoring unstaged changes to partially staged files...
✔ Cleaning up temporary files...
[main bf38a3f] test
 1 file changed, 1 insertion(+), 1 deletion(-)
```
