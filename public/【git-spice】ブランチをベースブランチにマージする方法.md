---
title: 【git-spice】ブランチをベースブランチにマージする方法
tags:
  - git-spice
private: false
updated_at: '2025-08-19T23:18:43+09:00'
id: 7e27b5b066437653a39a
organization_url_name: null
slide: false
ignorePublish: false
---
`gs branch fold`を使用すると現在のブランチをそのベースブランチにマージし、元のブランチを削除できます。

## 基本的な構文

```bash
gs branch fold [flags]
```

## 動作

以下のようなブランチスタックがあるとします。

```
    ┌── C
  ┌─┴ B ◀ (現在のブランチ)
┌─┴ A
trunk
```

`gs branch fold`を実行すると

```
  ┌── C
┌─┴ A (BのコミットがAにマージされる)
trunk
```

- ブランチBのコミットがブランチAにマージされます
- ブランチBは削除されます
- ブランチCは自動的にブランチAを指すように更新されます

## フラグ

### `--branch=NAME`

対象となるブランチを指定します。このフラグを使用すると、現在のブランチ以外のブランチをマージできます。

```bash
# 現在のブランチをfoldする（デフォルト）
gs branch fold

# 特定のブランチをfoldする
gs branch fold --branch feature-branch
```

## 参考

- [git-spice CLI Reference](https://abhinav.github.io/git-spice/cli/reference/)
