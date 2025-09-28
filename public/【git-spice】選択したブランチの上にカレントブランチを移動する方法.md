---
title: 【git-spice】選択したブランチの上にカレントブランチを移動する方法
tags:
  - 'git-spice'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 移動方法

`gs branch onto`で現在のブランチを洗濯したブランチの上に移動できます。

```bash
# 対話式でベースブランチを選択
gs branch onto
```

ブランチの表示順は以下のコマンドで設定できます。

```bash
# 現在のユーザーのオプションを設定する
$ git config --global spice.branchPrompt.sort <value>

# 現在のリポジトリのオプションを設定する
$ git config --local spice.branchPrompt.sort <value>
```

## 参考

https://abhinav.github.io/git-spice/cli/reference/#gs-branch-onto

https://abhinav.github.io/git-spice/cli/config/#spicebranchpromptsort

