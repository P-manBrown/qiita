---
title: 【git-spice】ブランチを別のブランチの上に移動する方法
tags:
  - 'git-spice'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## `gs branch onto` - 単一ブランチの移動

現在のブランチを別のブランチに移動する最も基本的なコマンドです。

```bash
# 対話式でベースブランチを選択
gs branch onto

# 直接ベースブランチを指定
gs branch onto main

# 特定のブランチを移動（現在のブランチでない場合）
gs branch onto main --branch feature-A
```

例えば、以下のようなスタック構造があるとします

```
    ┌── C
  ┌─┴ B ◀  (現在のブランチ)
┌─┴ A
main
```

`gs branch onto main`を実行すると

```
    ┌── B ◀  (移動後)
    │ ┌── C
    ├─┴ A
    main
```

ブランチBが`main`に移動し、ブランチCはAの上に残ります。

https://abhinav.github.io/git-spice/cli/reference/#gs-branch-onto

## `gs upstack onto` - アップスタック全体の移動

現在のブランチとその上にあるすべてのブランチ（アップスタック）を一緒に移動します。

```bash
# 対話式でベースブランチを選択
gs upstack onto

# 直接ベースブランチを指定
gs upstack onto main

# 特定のブランチから開始
gs upstack onto main --branch feature-A
```

同じスタック構造で`gs upstack onto main`を実行すると

```
    ┌── C                 ┌── C
  ┌─┴ B ◀               ┌─┴ B ◀
┌─┴ A                   ├── A
main                    main
```

ブランチBとその上のブランチCが一緒に`main`に移動します。

https://abhinav.github.io/git-spice/cli/reference/#gs-upstack-onto
