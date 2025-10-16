---
title: 【git-spice】コミットを修正する方法
tags:
  - git-spice
private: false
updated_at: '2025-08-06T22:55:03+09:00'
id: 2f4eca5c88043b59f30b
organization_url_name: null
slide: false
ignorePublish: false
---
## 修正方法

`gs commit amend`を使用して現在のコミットを修正できます。

### コマンド構文

```bash
gs commit amend [flags]
# または短縮形
gs c a [flags]
```

### 基本的な使用例

```bash
# ファイルを修正してステージ
git add modified_file.py

# コミットを修正（上位ブランチも自動で再スタック）
gs commit amend
```

## 利用可能なオプション

`gs commit amend`では以下のオプションが使用できます。

### `-a, --all`

コミット前にすべての変更を自動的にステージします。

```bash
# 修正したファイルを自動でステージしてからamend
gs commit amend -a
```

### `-m, --message=MSG`

コミットメッセージを指定します。エディタを開くことなく、直接メッセージを設定できます。

```bash
gs commit amend -m "修正: バグを修正しユーザビリティを改善"
```

### `--no-edit`

コミットメッセージを編集せず、既存のメッセージをそのまま使用します。

```bash
# メッセージはそのままで、変更内容だけを追加
gs commit amend --no-edit
```

### `--allow-empty`

変更がない場合でもコミットを作成します。

```bash
# 変更がなくてもコミットを修正
gs commit amend --allow-empty
```

### `--no-verify`

pre-commitやcommit-msgフックをバイパスします。

```bash
# フックをスキップして高速にamend
gs commit amend --no-verify
```

## 参考

https://abhinav.github.io/git-spice/cli/reference/#gs-commit-amend
