---
title: 【Git】削除したファイルを復元する方法
tags:
  - Git
private: false
updated_at: '2025-03-12T23:55:09+09:00'
id: 7fa99b3cf8ffb656ddb1
organization_url_name: null
slide: false
ignorePublish: false
---
## ファイルを削除したコミットを探す

まず、削除されたファイルが含まれていたコミットを特定します。以下のコマンドを使用します:

```terminal
git log --diff-filter=D --summary
```

このコマンドは、削除（D）されたファイルのコミット履歴を表示します。

また、以下のコマンドでも検索できます。

```terminal
git log -- <ファイルパス>
```

例:

```terminal
git log -- src/main.py
```

詳細については [git-log](https://git-scm.com/docs/git-log) を参照してください。

## ファイルの復元

特定したコミットからファイルを復元します。以下のコマンドを使用します:

```terminal
git checkout <コミットハッシュ> -- <ファイルパス>
```

- `<コミットハッシュ>`: ファイルが削除されたコミットのハッシュ
- `<ファイルパス>`: 復元したいファイルのパス

例:

```terminal
git checkout a1b2c3d4 -- src/main.py
```

詳細は[git-checkout](https://git-scm.com/docs/git-checkout) を参照してください。

## 復元したファイルをコミットする

ファイルを復元したら、通常通りにステージングしてコミットします。

```terminal
git add <ファイルパス>
git commit -m "<コミットメッセージ>"
```

例:

```terminal
git add src/main.py
git commit -m "src/main.py を復元"
```
