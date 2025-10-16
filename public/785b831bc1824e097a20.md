---
title: 【Git】リモートブランチを削除する方法
tags:
  - Git
private: false
updated_at: '2025-09-25T21:11:41+09:00'
id: 785b831bc1824e097a20
organization_url_name: null
slide: false
ignorePublish: false
---
## 削除方法

以下のコマンドでリモートブランチを削除できます。

```bash
git push origin --delete <ブランチ名>
```

## 例

`feature/sample`ブランチを削除する場合には以下のようになります。

```bash
git push origin --delete feature/sample
```

## 確認方法

```bash
git branch -r
```

または

```bash
git branch -a
```
