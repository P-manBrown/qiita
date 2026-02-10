---
title: 【Zed】開いているファイルのディレクトリでターミナルを開く方法
tags:
  - ZedEditor
private: false
updated_at: '2026-02-10T19:56:00+09:00'
id: 7f841374d9d765ccdea7
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

Zed v0.223.0から、現在開いているファイルと同じディレクトリでターミナルを起動する機能が追加されました。

## 設定方法

`settings.json` に以下の設定を追加します。

```json
{
  "terminal": {
    "working_directory": "current_file_directory"
  }
}
```

## 動作仕様

この設定により、新しいターミナルを開く際に以下の順序でディレクトリが決定されます。

1. **現在開いているファイルのディレクトリ**（最優先）
2. プロジェクトディレクトリ（ファイルが開かれていない場合）
3. 最初のワークスペースディレクトリ（上記がない場合）

## 例

たとえば `/path/to/project/src/components/Button.tsx` を開いている場合、ターミナルは `/path/to/project/src/components/` ディレクトリで起動します。

## 従来の動作

`working_directory` のデフォルト値は以下のいずれかです。

- `"project"`: プロジェクトルートで開く
- `"first_project_directory"`: 最初のワークスペースディレクトリで開く

新しいオプション `"current_file_directory"` を使用することで、より直感的なワークフローが実現できます。

## 参考

https://zed.dev/releases/preview/0.223.0

https://github.com/zed-industries/zed/pull/47739
