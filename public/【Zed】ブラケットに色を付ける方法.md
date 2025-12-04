---
title: 【Zed】ブラケットに色を付ける方法
tags:
  - ZedEditor
private: false
updated_at: '2025-12-04T23:54:52+09:00'
id: 65f288f9adc7d27694da
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

### 言語ごとに適用

`settings.json`に以下を追加します。

```json
{
  "languages": {
    "JavaScript": {
      "colorize_brackets": true
    },
    "Python": {
      "colorize_brackets": true
    }
  }
}
```

### 全言語に適用

すべての言語で有効にする場合は`settings.json`に以下を追記します。

```json
{
  "colorize_brackets": true
}
```

## カスタマイズ

### 色のカスタマイズ

テーマのアクセントカラーを上書きできます。

```json
{
  "theme_overrides": {
    "One Dark": {
      "accents": [
        "#ff69b4",
        "#7fff00",
        "#ff1493",
        "#00ffff",
        "#ff8c00",
        "#9400d3"
      ]
    }
  }
}
```

### 特定の括弧を除外

言語の`brackets.scm`を編集して特定の括弧ペアを除外できます。

```scheme
; 除外前
("\"" @open "\"" @close)

; 除外後
(("\"" @open "\"" @close) (#set! rainbow.exclude))
```

## 参考

https://github.com/zed-industries/zed/pull/43172
