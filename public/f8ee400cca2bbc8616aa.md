---
title: 【git-spice】gs branch checkoutのリストに未追跡ブランチを含めるか設定する方法
tags:
  - git-spice
private: false
updated_at: '2025-09-02T00:04:52+09:00'
id: f8ee400cca2bbc8616aa
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

### 基本設定

未追跡ブランチをリストに含めるには、以下の設定オプションを使用します。

```bash
# ユーザーレベル（グローバル）で設定
git config --global spice.branchCheckout.showUntracked true

# リポジトリレベル（ローカル）で設定
git config --local spice.branchCheckout.showUntracked true
```

### 設定値

`spice.branchCheckout.showUntracked`は以下の値を受け付けます。

- `true`：未追跡ブランチをリストに表示する
- `false`：未追跡ブランチをリストに表示しない（デフォルト）

## 参考

https://abhinav.github.io/git-spice/cli/config/#spicebranchcheckoutshowuntracked
