---
title: 【Obsidian】Spaced Repetition の使い方
tags:
  - Obsidian
private: false
updated_at: '2024-09-15T22:05:54+09:00'
id: 76b3abe3f8d7a8ca0dee
organization_url_name: null
slide: false
ignorePublish: false
---
## Spaced Repetitionとは

Spaced Repetitionは、フラッシュカードとノートのレビューを通じて間隔反復学習をサポートしてくれるObisidianのプラグインです。

https://github.com/st3v3nmw/obsidian-spaced-repetition

## インストール

Obsidianのコミュニティプラグインセクションからインストールできます。

![スクリーンショット 2024-09-14 23.08.31.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/ee635a79-a736-e5f5-77fa-8209a32a7df4.png)

## フラッシュカード

### 作成

`#flashcards`のタグをつけるとフラッシュカードとして認識されます。`#flashcards/deckA`のように階層を分け、分類することもできます。

```md
#flashcards/deckA
```

単一行のフラッシュカードを作成するには質問と答えを`::`で区切り、`質問::答え`のように記述します。

```md
#flashcards/deckA
質問1::回答1
```

上記のように記述すると以下のようなフラッシュカードが作成されます。

![スクリーンショット 2024-09-14 23.19.16のコピー.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/60f2a7b0-0559-3f71-b967-45f0c5da522e.png)


![スクリーンショット 2024-09-14 23.19.35のコピー.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/580b3a64-70f2-8fb3-8e43-56bc4b4b4d3f.png)

複数行のフラッシュカードを作成するには`?`で区切ります。

```md
#フラッシュカード/deckA 
複数行の
質問
?
複数行の
回答
```

上記のように記述した場合、以下のようなフラッシュカードが作成されます。

![スクリーンショット 2024-09-14 23.26.23のコピー.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/2558e1a1-e924-7bae-928a-c693ff7efd21.png)

![スクリーンショット 2024-09-14 23.26.38のコピー.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/2aafcdf1-e5f9-7f0e-a893-28137588eb8d.png)

穴埋めのフラッシュカードを作成するには穴埋めにしたい単語を`==`で囲みます。

```md
#フラッシュカード/deckA 
==穴埋め==のフラッシュカード
```

![スクリーンショット 2024-09-14 23.32.52のコピー.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/b7fea7ad-0b8d-ae79-edbc-cf27d18d144e.png)

![スクリーンショット 2024-09-14 23.33.08のコピー.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/830ce1c3-37e1-6dca-5389-6fba75dc72e1.png)

なお、上述の`#flashcards`や`::`や`?`、`==`の記号はすべて設定で任意のものに変更できます。

### レビュー

コマンドパレットから「Spaced Repetition： すべてのノートからフラッシュカードをレビューする」を実行して作成したフラッシュカードをレビューします。

![スクリーンショット 2024-09-14 23.42.51.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/33208477-11dc-30ad-4f55-1a43ae355ecc.png)

回答を表示した際、カード下部にボタンが表示されます。

![68747470733a2f2f71696974612d696d6167652d73746f72652e73332e61702d6e6f727468656173742d312e616d617a6f6e6177732e636f6d2f302f323334323434332f38333063653163332d333765312d366463612d353338392d3666626137356463373265312e706e67のコピー.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/161ac012-2144-d31b-d232-b1319bb5a4f8.png)


このボタンに記載されている日数後に再度レビュー可能になります。

## ノート

ノート自体をフラッシュカードのように使用することもできます。

ノートに`#review`というタグをつけるとレビュー対象として認識されます。

コマンドパレットから「Spaced Repetition: Open Notes Review Queue in sidebar」を実行するとサイドバーにレビュー対象ノートの一覧が表示されます。

![スクリーンショット 2024-09-14 23.51.59.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/6450d87d-a053-e03f-0a21-a50eae7f1d01.png)


それぞれのノートを表示し、コマンドパレットなどからフラッシュカードと同様に「Hard」「Good」「Easy」のいずれかで評価します。
「Hard」「Good」「Easy」のうちどれを選択したかで次回レビューまでの感覚が変化します。

## 参考

https://www.stephenmwangi.com/obsidian-spaced-repetition/
