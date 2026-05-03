---
title: 【Zed】コードレンズを有効化する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-05-04T00:00:05+09:00'
id: 579a9011ecf916d81b1e
organization_url_name: null
slide: false
ignorePublish: false
---

## コードレンズとは

コードレンズ（Code Lens）とは、ソースコードの関数やクラスなどの定義の上に、参照数・テスト実行ボタン・実装数といった情報をインラインで表示する機能です。VSCode や JetBrains 系 IDE などでよく見られる機能で、コードを読む際に役立つ補足情報をエディタ内で直接確認できます。

Zed では、この機能が長らくリクエストされていましたが、2026年4月22日にマージされたPRにて正式にサポートされました。

https://github.com/zed-industries/zed/pull/54100

Zed Preview 1.1.2 のリリースノートにも、コードレンズのサポートが記載されています。

https://zed.dev/releases/preview/1.1.2

## デフォルトの挙動

コードレンズはデフォルトで**無効（`"off"`）**になっています。有効にするには、設定ファイル（`settings.json`）を編集するか、アクションからトグルする必要があります。

## 設定方法

### settings.json で有効化する

`settings.json` に `"code_lens"` の設定を追加します。取りうる値は以下の3つです。

```json
// コードレンズを表示しない（デフォルト）
{
  "code_lens": "off"
}
```

```json
// コードの要素の上にコードレンズを表示する
{
  "code_lens": "on"
}
```

```json
// コードアクションのメニュー内にコードレンズを表示する
{
  "code_lens": "menu"
}
```

通常のコードレンズ表示（VSCode のような見た目）を使いたい場合は `"on"` を指定してください。

### アクションからトグルする

コマンドパレット（`Cmd+Shift+P`）から `editor: toggle code lens` を実行することでも、コードレンズのオン/オフを切り替えられます。

## 言語サーバーの追加設定について

コードレンズは、ランゲージサーバー（LSP）がコードレンズ情報を提供することで初めて表示されます。Zed 側でコードレンズを有効にしただけでは表示されないケースがあり、その場合は言語サーバー側の設定も必要になります。

たとえば Rust の場合、`rust-analyzer` に対して以下のような追加設定を行うことで、参照数などのコードレンズが表示されるようになります。

```json
{
  "code_lens": "on",
  "lsp": {
    "rust-analyzer": {
      "initialization_options": {
        "lens": {
          "enable": true,
          "references": {
            "enable": true
          },
          "implementations": {
            "enable": true
          }
        }
      }
    }
  }
}
```

Go の場合は `gopls` が標準でコードレンズをサポートしており、追加設定なしで参照数などが表示されます。

