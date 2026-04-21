---
title: 【Zed】Git Graphを開く方法
tags:
  - ZedEditor
private: false
updated_at: '2026-04-21T19:51:57+09:00'
id: 9bfbe2eb735b4fe8f67d
organization_url_name: null
slide: false
ignorePublish: false
---

## Git Graph とは

Git Graph は、リポジトリのコミット履歴をグラフ形式で視覚的に確認できる機能です。ブランチの分岐やマージの流れを一目で把握できるため、チーム開発や複雑なブランチ構成を持つプロジェクトで特に役立ちます。

Zed では v0.231 から Git Graph が正式に利用可能になりました。

## Git Graph を開く方法

Git Graph を開くには、以下の 2 通りの方法があります。

### 方法 1：Git パネルのボタンから開く

Git パネルの下部に Git Graph を開くためのボタンが配置されています。これをクリックすることで開けます。

### 方法 2：コマンドパレットから開く

コマンドパレット（`Cmd+Shift+P` / `Ctrl+Shift+P`）を開き、以下のアクションを実行します。

```
git graph: Open
```

どちらの方法でも同じ Git Graph パネルが開きます。

## Git Graph で確認できること

Git Graph を開くと、現在のリポジトリのコミット履歴がグラフ形式で表示されます。主に以下の情報を視覚的に確認できます。

コミットのハッシュ・メッセージ・日時・作成者といった基本情報のほか、ブランチの分岐とマージの流れをグラフで把握できます。複数のブランチが絡み合った状況でも、どのコミットがどのブランチに属しているかを直感的に理解できます。

## 参考

https://github.com/zed-industries/zed/pull/53002

https://github.com/zed-industries/zed/pull/52972
