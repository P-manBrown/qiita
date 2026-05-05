---
title: 【Zed】ターミナルにBEL文字が出力された際に音を鳴らす方法
tags:
  - ZedEditor
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

## はじめに

Zed v1.1.2（Preview）にて、ターミナルでBEL文字（`\a`）が出力された際にシステムの警告音を鳴らす機能が追加されました。

この機能は `terminal.bell` 設定で有効にできます。デフォルトでは無効になっているため、本記事では設定方法と動作について解説します。

## BEL文字とは

BEL文字（ベル文字）は、ASCIIコード `0x07` に対応する制御文字で、`\a` と表記されます。もともとはテレタイプ端末のベル（鈴）を鳴らすために使われていた文字で、現在のターミナルエミュレータでもアラート音を出力するために使用されます。

多くのターミナルアプリケーション（iTerm2、Ghostty、WezTermなど）ではBEL文字を受け取ると音を鳴らす機能が標準で搭載されていますが、ZedはこのPRまでその機能がありませんでした。

## 設定方法

`settings.json` に以下の設定を追加します。

```json
{
  "terminal": {
    "bell": "system"
  }
}
```

`"system"` を指定することで、BEL文字を受信した際にOSデフォルトの警告音が鳴ります。

音を無効にしたい場合は、以下のように設定します。

```json
{
  "terminal": {
    "bell": "off"
  }
}
```

### 設定をUIから変更する方法

設定UIを開くには `cmd + ,`（macOS）または `ctrl + ,`（Windows/Linux）でSettings画面を開き、Terminalセクションの `bell` 項目を変更することもできます。

## 動作確認

設定後、Zedのターミナルを開いて以下のコマンドを実行してみましょう。

```bash
echo -e "\a"
```

または

```bash
printf "\a"
```

`"system"` を設定していれば、コマンド実行時にシステムの警告音が鳴ります。

## 活用シーン

BEL文字を活用することで、長時間かかる処理の完了を音で通知させることができます。

たとえば、時間のかかるコマンドの末尾に `&& printf "\a"` を追加しておくと、処理が完了したタイミングで音が鳴り、別の作業をしていても気づくことができます。

```bash
# ビルドが完了したら音を鳴らす例
bundle exec rails db:migrate && printf "\a"

# テストが完了したら音を鳴らす例
bundle exec rspec && printf "\a"

# npmのインストール完了を通知する例
npm install && printf "\a"
```

エイリアスを設定しておくと便利です。

```bash
# .zshrc や .bashrc に追加
alias bell='printf "\a"'

# 使用例
npm install && bell
```

## 参考

https://github.com/zed-industries/zed/pull/53752

https://zed.dev/releases/preview/1.1.2
