---
title: 【git-spice】ログにレビューコメントの数を表示する方法
tags:
  - git-spice
private: false
updated_at: '2026-04-15T01:37:32+09:00'
id: 788fc6b3a4509251ecd4
organization_url_name: null
slide: false
ignorePublish: false
---
## `-c` / `--cr-comments` フラグ

`gs log short` / `gs log long` には、`-c` または `--cr-comments` というフラグが用意されています。

```bash
gs log short --cr-comments
# または短縮形
gs ls -c

gs log long --cr-comments
# または短縮形
gs ll -c
```

このフラグを付けると、各ブランチに対応するPRのレビューコメントの解決数（resolved / total）がログに表示されます。たとえば、3件中2件のコメントが解決済みの場合は次のように表示されます。

```
  ┌── feature/api-refactor  #42  2/3 comments
  ├── feature/add-login      #41  ✓
◀─┴── feature/setup-db      #40  ✓
main
```

レビュアーとのやり取りが多いスタックで、どのブランチにまだ未解決のコメントが残っているかを一目で把握できます。

## 設定ファイルで常に有効にする

```bash
# 現在のリポジトリに設定
git config --local spice.log.crComments true

# 全リポジトリに設定（グローバル）
git config --global spice.log.crComments true
```

`spice.log.crComments` を `true` にしておくことで、`-c` フラグなしでも常にコメント数が表示されるようになります。

同様に、PR ステータスを常に表示したい場合は以下のように設定します。

```bash
git config --global spice.log.crStatus true
```

## 参考

https://abhinav.github.io/git-spice/cli/reference/#log

https://abhinav.github.io/git-spice/cli/config/#spicelogcrcomments
