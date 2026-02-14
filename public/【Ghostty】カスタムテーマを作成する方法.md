---
title: 【Ghostty】カスタムテーマを作成する方法
tags:
  - ghostty
private: false
updated_at: '2026-02-14T23:57:12+09:00'
id: e4fd6c2f188871d40412
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

カスタムテーマを作成する際は、以下のオプションを設定します。

- `background` - 背景色
- `foreground` - 前景色（テキスト色）
- `cursor-color` - カーソルの色
- `selection-foreground` - 選択テキストの色
- `selection-background` - 選択範囲の背景色
- `palette` - ANSIカラーパレット（0-15の16色）

## テーマファイルの例

以下は完全なテーマファイルの例です。
```
palette = 0=#51576d
palette = 1=#e78284
palette = 2=#a6d189
palette = 3=#e5c890
palette = 4=#8caaee
palette = 5=#f4b8e4
palette = 6=#81c8be
palette = 7=#a5adce
palette = 8=#626880
palette = 9=#e67172
palette = 10=#8ec772
palette = 11=#d9ba73
palette = 12=#7b9ef0
palette = 13=#f2a4db
palette = 14=#5abfb5
palette = 15=#b5bfe2
background = #303446
foreground = #c6d0f5
cursor-color = #f2d5cf
cursor-text = #c6d0f5
selection-background = #626880
selection-foreground = #c6d0f5
```

## テーマファイルの配置場所

テーマファイルは以下のディレクトリに配置することで、名前で参照できます：

1. `$XDG_CONFIG_HOME/ghostty/themes`
2. `$PREFIX/share/ghostty/themes`

絶対パスを使用することも可能です。

## テーマの使用方法

作成したテーマは、設定ファイルで以下のように指定します。
```
theme = my-custom-theme
```

または絶対パスで指定します。
```
theme = /path/to/my-theme.conf
```

## ライト/ダークテーマの切り替え

システムの外観設定に応じて自動的にテーマを切り替えることも可能です：
```
theme = dark:Catppuccin Frappe,light:Catppuccin Latte
```

## テーマの読み込み順序

テーマファイルは**ユーザー設定の前に**読み込まれます。そのため、ユーザー設定で同じオプションを指定した場合、ユーザー設定が優先されます。これにより、テーマの色を部分的に上書きすることができます。
