---
title: 【Git】直前のコミットに変更を追加する方法
tags:
  - Git
private: false
updated_at: '2025-07-20T21:29:39+09:00'
id: dba7d08b5ffa029df968
organization_url_name: null
slide: false
ignorePublish: false
---
`git commit --amend` を使用すると直前のコミットに変更を追加できます。

## ステージング

追加したいファイルを `git add` します。

```bash
git add path/to/sample.txt
```

## 直前コミットへの追加

ステージングした状態で、`--amend` オプションを使ってコミットを修正します。

```bash
# コミットメッセージをそのまま使う場合
git commit --amend --no-edit

# コミットメッセージを変更したい場合
git commit --amend
# エディタが開くので、必要に応じてメッセージを書き換える
```

## リモートリポジトリへの反映

すでにリモートにプッシュ済みのコミットを書き換えた場合は、強制プッシュが必要です。

```bash
git push origin ブランチ名 --force-with-lease
```
