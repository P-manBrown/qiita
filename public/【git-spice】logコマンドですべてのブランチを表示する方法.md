---
title: 【git-spice】logコマンドですべてのブランチを表示する方法
tags:
  - 'git-spice'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## すべてのブランチを表示する方法

`-a`を使用するとすべてのブランチを表示できます。
使用しない場合には現在のスタックのブランチのみ表示されます。

```bash
gs log short -a
# または
gs log short --all

# 長い形式の場合
gs log long -a
# または
gs log long --all
```

## logコマンドの種類

git-spiceには2種類のlogコマンドがあります。

- **`gs log short`** (`gs ls`): ブランチのリストを表示
- **`gs log long`** (`gs ll`): ブランチとコミットの両方を表示

## 設定ファイルでデフォルト動作を変更

毎回`--all`フラグを付けたくない場合は、設定ファイルで変更できます。

```bash
git config spice.log.all true
```

この設定により、`gs log`コマンドがデフォルトですべてのブランチを表示するようになります。

## 参考

https://abhinav.github.io/git-spice/cli/reference/#log
