---
title: Jujutsuの使い方
tags:
  - Git
  - Jujutsu
private: false
updated_at: '2026-03-07T21:49:40+09:00'
id: 47c2dd2e1271047fd4ab
organization_url_name: null
slide: false
ignorePublish: false
---
## Jujutsuとは？

JujutsuはGitと互換性のある実験的なVCSです。コマンドラインツールは `jj` と呼ばれます。

既存のGitリポジトリをそのまま活用できるため、GitHubなどの既存ワークフローを捨てる必要はありません。`jj` はGitの上に乗る形で動作します。

## Gitとの主な違い

| 概念 | Git | Jujutsu |
|------|-----|---------|
| ステージング（インデックス）| ある | **ない** |
| 自動スナップショット | ない | **あり**（`jj` コマンド実行時に自動保存） |
| 過去コミットの修正 | `rebase -i` が必要 | `jj edit` で簡単に |
| コンフリクト時 | 作業が中断される | **コミットに記録されて継続できる** |
| ブランチ | 必須 | ブックマーク（任意） |

## インストールと初期設定

### インストール

```bash
# macOS（Homebrew）
brew install jj

# バージョン確認
jj --version
```

### 既存のGitリポジトリに導入する

`--colocate` オプションを使うと、`.git` ディレクトリを残したまま `jj` を使い始められます。既存のGitコマンドも引き続き使えます。

```bash
cd your-existing-git-repo
jj git init --colocate
```

## #ユーザー情報を設定する

```bash
jj config set --user user.name "Your Name"
jj config set --user user.email "you@example.com"
```

---

## 基本的な使い方

### ワーキングコピーの仕組み

Jujutsuには**ステージングエリアがありません**。代わりに、`jj` コマンドを実行するたびにワーキングコピーの状態が自動的にスナップショットとして記録されます。

```bash
# ファイルを編集する（git add は不要）
echo "Hello, Jujutsu!" > hello.txt

# 状態確認（git status に相当）
jj status
# Working copy changes:
# A hello.txt
# Working copy (@) : abc12345 (empty) (no description set)
```

### コミットメッセージを付ける（jj describe）

```bash
jj describe -m "Add hello.txt"
# Working copy (@) now at: abc12345 Add hello.txt
```

### 新しいコミットを作る（jj new）

```bash
jj new
# Working copy (@) now at: def67890 (empty) (no description set)
```

これが Git の「コミットして次の作業に移る」に相当します。

### 履歴を見る（jj log）

```bash
jj log
# @ def67890 you@example.com 2026-03-07 (empty) (no description set)
# ○ abc12345 you@example.com 2026-03-07 Add hello.txt
# ◆ main     origin/main
```

`@` は現在のワーキングコピーを示します。

### 過去のコミットを直接編集する（jj edit）

Gitで過去のコミットを修正するには `git rebase -i` が必要でした。Jujutsuでは `jj edit` で直接そのコミットに移動して編集できます。

```bash
# 現在の履歴
jj log
# @ mrx789    "Add feature C"
# ○ knt456    "Add feature B"  ← ここにバグがある
# ○ ztq123    "Add feature A"
# ◆ main

# feature B のコミットに移動して編集
jj edit knt456

# ファイルを修正する
echo "fixed content" > feature_b.txt

# 修正が自動的に knt456 に反映される
# 子孫コミット（mrx789）も自動的にリベースされる！
```

Jujutsuの強力な点は、**過去のコミットを編集すると、子孫コミットが自動的にリベースされる**ことです。Gitのように手動でリベースし直す必要はありません。

### コミットをまとめる（jj squash）

現在のコミットを親コミットにまとめたい場合は `jj squash` を使います。

```bash
# "fix typo" を直前のコミットにまとめる
jj log
# @ xyz999    "fix typo"
# ○ abc123    "Add user authentication"
# ◆ main

jj squash
# @ abc123    "Add user authentication"（fix typo の変更が取り込まれた）
# ◆ main
```

### インタラクティブに選択してまとめる

どの変更だけをまとめるか選びたい場合は `-i` オプションを使います。

```bash
jj squash -i
# diff エディタが開き、まとめたい変更を選択できる
```

### 別のコミットへ移動させる

特定のファイルの変更だけを別のコミットへ移動させることも可能です。

```bash
# feature.txt の変更を親コミットへ移動
jj squash feature.txt

# 特定コミットへ移動（--from と --into を指定）
jj squash --from @ --into abc123
```

### コミットを分割する（jj split）

1つのコミットに複数の変更が混在している場合、`jj split` で分割できます。

```bash
# 現在のコミットに機能追加とバグ修正が混在している
jj split
# インタラクティブなdiffエディタが開く
# → 機能追加の変更だけを選択して「最初のコミット」に
# → 残りのバグ修正が「2つ目のコミット」になる
```

実際のユースケース：

```bash
# 1つのコミットに機能実装とリンター警告の修正が入っていた場合
jj split
# → "Add user auth feature"（機能実装のみ）
# → "Fix linter warnings"（リンター修正のみ）
# という2つのきれいなコミットに分割できる
```

### 変更を適切なコミットに自動振り分ける（jj absorb）

これはJujutsuの中でも特に便利なコマンドです。ワーキングコピーの変更を、その行を最後に変更したコミットへ自動的に振り分けてくれます。

```bash
# スタック状のコミットに対して細かい修正をした後
jj log
# @ wip        (作業中の変更)
# ○ feat-c     "Add feature C"
# ○ feat-b     "Add feature B"
# ○ feat-a     "Add feature A"
# ◆ main

# 各変更を適切なコミットへ自動振り分け
jj absorb

# 結果：各ファイルの変更が「最後にそのファイルを変更したコミット」へ自動マージされる
```

Gitで同じことをしようとすると、各コミットに対して `git commit --fixup <ID>` を実行してから `git rebase --autosquash` を行う必要があります。`jj absorb` ならコマンド1つで完結します。

### コミットの間に新しいコミットを挿入する

「あのコミットの前に修正を入れておきたかった」という場面は `jj new -B`（Before）や `jj new -A`（After）で対応できます。

```bash
# feat-b の直前に新しいコミットを挿入
jj new -B feat-b
# → 新しい空コミットが feat-a と feat-b の間に作成される

# 修正を加えた後、元のコミットに戻る
jj edit @+
```

## Git コマンドとの対応表

| やりたいこと | Git | Jujutsu |
|-------------|-----|---------|
| 変更を確認 | `git status` | `jj status` |
| 差分を見る | `git diff` | `jj diff` |
| 履歴を見る | `git log` | `jj log` |
| コミットメッセージを設定 | `git commit -m` | `jj describe -m` |
| 新しいコミットを作る | `git add + git commit` | `jj new` |
| 過去のコミットを修正 | `git rebase -i` | `jj edit <id>` |
| コミットをまとめる | `git commit --amend` / `git rebase -i` | `jj squash` |
| コミットを分割 | `git add -p + git commit` | `jj split` |
| 変更を自動振り分け | `git commit --fixup + rebase --autosquash` | `jj absorb` |
| 操作を取り消す | `git reflog` で復元 | `jj undo` |
| リモートへプッシュ | `git push` | `jj git push` |

## 参考

https://docs.jj-vcs.dev/latest/

https://docs.jj-vcs.dev/latest/tutorial/

https://docs.jj-vcs.dev/latest/git-experts/

https://github.com/jj-vcs/jj
