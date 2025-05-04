---
title: 【Git】ローカルにないリモートブランチを取り込む方法
tags:
  - Git
  - 初学者
private: false
updated_at: '2025-04-14T15:45:18+09:00'
id: f4df2acec363156cdc9f
organization_url_name: null
slide: false
ignorePublish: false
---
## `git fetch`

まずリモート追跡ブランチが存在するか確認するために`git branch -r`を実行します。  

```terminal
git branch -r
```

この時点でリモート追跡ブランチが存在すれば`git fetch`は不要です。  
存在しない場合は`git fetch`で作成します。  

```terminal
git fetch
```

特定のブランチのリモート追跡ブランチのみ作成するには次のように実行します。  

```terminal
git fetch origin ブランチ名
```

## `git checkout`

ローカルブランチ名を指定してリモートブランチをチェックアウトします。  

```terminal
git checkout -b ブランチ名 origin/ブランチ名
```
