---
title: 【VSCode】GitHub Copilot ChatでWeb検索を使用する方法
tags:
  - VSCode
  - githubcopilot
  - githubcopilotchat
private: false
updated_at: '2024-10-31T19:49:11+09:00'
id: f5eb3efa1aea2dbf6780
organization_url_name: null
slide: false
ignorePublish: false
---
## Web Search for Copilotを使用する

Web Search for Copilotという拡張機能を導入するとGitHub Copilot ChatでWeb検索を使用して最新の情報が取得できるようになります。

### 拡張機能をインストール

以下のページの「インストール」をクリックして拡張機能をインストールします。

https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-websearchforcopilot

### TavilyのAPIキーを取得する

を使用するにはTavilyまたはBingのAPIキーが必要です。
今回はデフォルトで設定されているTavilyを使用します。
まず、[Tavily](https://tavily.com)にサインアップします。
サインアップすると以下の画面が表示され、TavilyのAPIを取得できます。

![スクリーンショット 2024-10-31 18.54.33.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/351d3163-b77e-3197-3277-a590b6cb21d6.png)

### APIキーを登録する

初めて`@websearch`を記述してGitHub Copilot Chatを使用した際に以下のようにAPIキーの入力欄が表示されます。

![スクリーンショット 2024-10-31 14.12.41.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/feb5f1a2-ad1a-feef-7d03-c4d18a9fe7ec.png)

上記で取得したAPIキーを入力して登録します。


以上で導入は完了です。
試しに「Next.jsの最新バージョンは何ですか」と質問すると2024年10月時点では15である旨の回答が得られました。

![スクリーンショット 2024-10-31 18.27.29.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/339555d1-b54c-73c5-f71d-8597bf04d34a.png)

## GitHub Copilotの設定を変更する

GitHub Copilotの設定を変更することで拡張機能なしでBingでのWeb検索が利用可能になります。
GitHub Copilotの設定画面の「Copilot access to Bing」を「Enabled」に変更します。

![スクリーンショット 2024-10-31 19.40.17.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/6c4b7a3e-dc1b-ac5a-7211-f28586798cc9.png)

https://github.blog/changelog/2024-10-29-web-search-in-github-copilot-chat-now-available-for-copilot-individual/

拡張機能を使用する場合と同様に「Next.jsの最新バージョンは何ですか」と質問すると以下のような回答でした。

![スクリーンショット 2024-10-31 19.38.24.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/2aafa969-189b-a6d7-fb36-b9c42ea7b07e.png)

質問の仕方を変えたところ正しい情報を得られました。

![スクリーンショット 2024-10-31 19.38.32.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/ddc49adc-327a-c6ab-0189-6adc63cfa188.png)

