---
title: 【Zed】プロジェクトパネルのソート順を設定する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-04-17T19:40:49+09:00'
id: ef1ff1ed61621fbe7167
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Zed のプロジェクトパネルでは、以前からファイルとディレクトリの並び順（`sort_mode`）を設定できましたが、新たに **`sort_order`** という設定が追加されました。これにより、ファイル名の比較方法（大文字・小文字の扱い、Unicodeの扱いなど）を細かくコントロールできるようになりました。

この記事では `sort_order` の各オプションと設定方法を解説します。

## `sort_mode` と `sort_order` の違い

まず、混同しやすい 2 つの設定を整理します。

`sort_mode` はファイルとディレクトリをどのグループに分けるかを制御します。`directories_first`（ディレクトリを先に表示）、`mixed`（混在）、`files_first`（ファイルを先に表示）の 3 種類があります。

`sort_order` は各グループ内でのファイル名の比較方法を制御します。大文字・小文字の優先度や、数値の扱い方などを指定できます。

2 つの設定は組み合わせて使うもので、例えば「ディレクトリを先に表示しつつ、名前は大文字優先でソートする」といった指定が可能になりました。

## `sort_order` のオプション一覧

### `default`（デフォルト）

大文字・小文字を区別しない自然順ソートで、同名の場合は小文字が優先されます。また、`file2` が `file10` より前に並ぶような自然順（数値を数値として比較）が適用されます。多くの場面でこのデフォルト動作が適切です。

### `upper`

大文字で始まるファイル・フォルダが、小文字で始まるものより前に表示されます。各グループ内では大文字・小文字を区別しない自然順ソートが適用されます。ドットで始まる名前（`.gitignore` など）は両グループより前に並びます。

例:
```
.gitignore
README.md
components/
src/
app.ts
index.ts
```

### `lower`

`upper` の逆で、小文字で始まるファイル・フォルダが先に表示されます。ドットで始まる名前は両グループより前です。

例:
```
.gitignore
app.ts
index.ts
src/
README.md
components/
```

### `unicode`

純粋な Unicode コードポイント順で比較します。大文字・小文字の折りたたみや自然数ソートは行われません。ASCII の大文字（A–Z）は小文字（a–z）より前に並び、アクセント付き文字は ASCII 文字より後に来ます。OS のファイルシステムに近い素の順序が必要な場合に使えます。

## 設定方法

Zed の設定ファイル（`settings.json`）に以下のように記述します。

```json
{
  "project_panel": {
    "sort_mode": "directories_first",
    "sort_order": "default"
  }
}
```

`sort_order` に指定できる値は `"default"`、`"upper"`、`"lower"`、`"unicode"` の 4 種類です。

### 設定例：ディレクトリ優先 ＋ 大文字優先

```json
{
  "project_panel": {
    "sort_mode": "directories_first",
    "sort_order": "upper"
  }
}
```

### 設定例：混在表示 ＋ Unicode 順

```json
{
  "project_panel": {
    "sort_mode": "mixed",
    "sort_order": "unicode"
  }
}
```

## 参考

https://github.com/zed-industries/zed/pull/50221
