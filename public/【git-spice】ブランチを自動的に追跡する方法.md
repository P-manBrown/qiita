---
title: 【git-spice】ブランチを自動的に追跡する方法
tags:
  - git-spice
private: false
updated_at: '2026-04-15T22:50:15+09:00'
id: 44022966bb10f1101f69
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

git-spice でブランチを切り替える際、そのブランチが git-spice に追跡されていない場合、デフォルトでは確認プロンプトが表示されます。

```
$ gs branch checkout mybranch
WRN mybranch: branch not tracked
Do you want to track this branch now?: [Y/n]
```

この挙動は `spice.branchCheckout.trackUntracked` という設定で変更できます。自動追跡を有効にすることで、毎回プロンプトに答える手間を省けます。

## spice.branchCheckout.trackUntracked とは

`gs branch checkout` で未追跡のブランチに切り替えたとき、そのブランチを git-spice が自動的に追跡するかどうかを制御する設定項目です。

設定できる値は以下の3つです。

| 値 | 動作 |
|---|---|
| `prompt`（デフォルト） | 確認プロンプトを表示する |
| `always` または `true` | プロンプトなしで自動的に追跡する |
| `never` または `false` | 追跡せず、プロンプトも表示しない |

## 設定方法

### 全ユーザー共通（グローバル設定）

自分のすべてのリポジトリで自動追跡を有効にしたい場合は `--global` フラグを使います。

```bash
git config --global spice.branchCheckout.trackUntracked always
```

### 特定のリポジトリのみ（ローカル設定）

特定のリポジトリだけに設定したい場合は `--local` フラグを使います。

```bash
git config --local spice.branchCheckout.trackUntracked always
```

### プロンプトを完全に無効化したい場合

追跡もせず、プロンプトも出したくない場合は `never` を指定します。

```bash
git config --global spice.branchCheckout.trackUntracked never
```

## 動作確認

設定後、未追跡のブランチに切り替えると挙動が変わります。

`always` に設定した場合、確認なしで即座に追跡が開始されます。

```bash
$ gs branch checkout feature/new-ui
# プロンプトなしでブランチが追跡される
```

`never` に設定した場合、警告もプロンプトも表示されず、ブランチの追跡はスキップされます。

## 参考

https://abhinav.github.io/git-spice/cli/config/#spicebranchcheckouttrackuntracked
