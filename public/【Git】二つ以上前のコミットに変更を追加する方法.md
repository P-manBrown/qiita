---
title: 【Git】二つ以上前のコミットに変更を追加する方法
tags:
  - 'Git'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
インタラクティブリベースを使用した方法

## インタラクティブリベースを開始

```bash
git rebase -i HEAD~n
```

`n`は編集したいコミットを含む過去のコミット数です。例えば、3つ前のコミットを編集したい場合は：

```bash
git rebase -i HEAD~3
```

## 編集するコミットを選択

エディターが開いて以下のような画面が表示されます。

```
pick abc1234 コミットメッセージ
pick def5678 コミットメッセージ
pick ghi9012 コミットメッセージ
```

編集したいコミットの `pick` を `edit` に変更します：

```
edit abc1234 コミットメッセージ
pick def5678 コミットメッセージ
pick ghi9012 コミットメッセージ
```

## ファイルを追加

変更を保存してエディターを閉じます。
新しいファイルを追加します。

```bash
# ファイルを作成または追加
echo "新しい内容" > new_file.txt

# ファイルをステージング
git add new_file.txt

# コミットを修正（--amend を使用）
git commit --amend
```

## リベースを続行

```bash
git rebase --continue
```

## 例

3つ前のコミットに `README.md` を追加したい場合：

```bash
# 1. インタラクティブリベースを開始
git rebase -i HEAD~3

# 2. エディタで該当するコミットを edit に変更して保存

# 3. README.md を作成
echo "# プロジェクト概要" > README.md

# 4. ファイルを追加
git add README.md

# 5. コミットを修正
git commit --amend

# 6. リベースを続行
git rebase --continue
```

:::note warn
注意
既にプッシュしたコミットの場合は `git push --force-with-lease` する必要があります。
:::

## 中断する場合

もし途中で問題が発生した場合は、以下のコマンドで元に戻せます。

```bash
git rebase --abort
```

