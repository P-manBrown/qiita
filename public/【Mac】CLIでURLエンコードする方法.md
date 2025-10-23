---
title: 【Mac】CLIでURLエンコードする方法
tags:
  - 'Mac'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## jqを使う方法

```bash
$ echo "テスト" | jq -sRr '@uri'
%E3%83%86%E3%82%B9%E3%83%88%0A
```

- `-s` (slurp): 入力全体を1つの文字列として読み込む
- `-R` (raw-input): 入力をJSON文字列ではなく生のテキストとして扱う
- `-r` (raw-output): 出力時にJSONの引用符を削除
- `@uri`: URLエンコード用のフォーマット関数

### jqのインストール

jqは以下のコマンドでインストールできます。

```bash
brew install jq
```

## Pythonを使う方法

```bash
$ echo "テスト" | python3 -c "import sys, urllib.parse; print(urllib.parse.quote(sys.stdin.read().strip()))"
%E3%83%86%E3%82%B9%E3%83%88
```
