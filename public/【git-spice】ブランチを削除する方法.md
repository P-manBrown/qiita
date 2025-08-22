---
title: 【git-spice】ブランチを削除する方法
tags:
  - 'git-spice'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
`gs branch delete`を使用するとgit-spiceで管理されているブランチを削除できます。

## コマンド構文

```bash
gs branch delete [<branches> ...] [flags]
```

または

```bash
gs b d [<branches> ...] [flags]
gs b rm [<branches> ...] [flags]
```

## 動作

- ブランチ名が指定されない場合、プロンプトで削除対象のブランチを選択できます
- 指定されたブランチとそのコミットがスタックから削除されます
- 削除されたブランチの上にあるブランチは、利用可能な下流のブランチにリベースされます

以下のようなスタック構造があり、

```
    ┌── C
  ┌─┴ B
┌─┴ A
trunk
```

ブランチBを削除すると

```bash
gs branch delete B
```

結果は以下のようになります。

```
  ┌── C
┌─┴ A
trunk
```

ブランチCは自動的にブランチAにリベースされ、スタック構造が保持されます。

## 例

### 対話的な削除

ブランチ名を指定せずに実行すると、削除対象のブランチを選択するプロンプトが表示されます。

```bash
gs branch delete
```

### 特定のブランチを削除

```bash
gs branch delete feature-branch
```

### 強制削除

安全チェックを回避して強制的に削除します。

```bash
gs branch delete feature-branch --force
```
