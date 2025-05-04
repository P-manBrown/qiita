---
title: 【Git】git diffコマンドについて
tags:
  - Git
  - 初学者
private: false
updated_at: '2023-02-16T23:53:20+09:00'
id: 01ffbc704aeea5874efe
organization_url_name: null
slide: false
ignorePublish: false
---
## リモートとの差分

```
$ git diff HEAD..リモート名/ブランチ名
```
```
$ git diff リモート名/ブランチ名..HEAD
```

## 直近のコミットの差分

```bash
git diff HEAD^..HEAD
```

## ブランチ間の差分

```bash
git diff ブランチA..ブランチB
```

## コミット間の差分

```bash
git diff 変更前のSHA..変更後のSHA
```

## 特定のファイルの差分
```bash
git diff -- ファイルパス
```
```bash
git diff ブランチA..ブランチB -- 対象のファイルパス
```


## ファイル名のみ出力

```bash
git diff --name-only
```
