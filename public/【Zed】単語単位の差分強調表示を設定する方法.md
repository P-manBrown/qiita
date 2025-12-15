---
title: 【Zed】単語単位の差分強調表示を設定する方法
tags:
  - ZedEditor
private: false
updated_at: '2025-12-15T20:09:33+09:00'
id: 9bbcfe5d8007d7e2df8b
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`settings.json`に以下の設定を追加します。

```json
{
  "languages": {
    "JavaScript": {
      "word_diff_enabled": true
    }
  }
}
```

すべての言語に対して設定するには以下のように記述します。

```json
{
  "word_diff_enabled": true
}
```

- `true`: 単語単位の差分強調表示を有効にする(デフォルト)
- `false`: 単語単位の差分強調表示を無効にする

## 参考

https://github.com/zed-industries/zed/pull/43269
