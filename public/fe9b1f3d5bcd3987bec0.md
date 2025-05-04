---
title: 【VSCode】VSCodeVimでカーソル移動した際に折りたたみが展開されないようにする
tags:
  - VSCode
private: false
updated_at: '2024-06-07T23:59:49+09:00'
id: fe9b1f3d5bcd3987bec0
organization_url_name: null
slide: false
ignorePublish: false
---
## 状況

カーソルを `j`, `k`で移動させ、折りたたみを通過した際に以下のように展開されてしまいました。

![画面収録 2024-06-07 23.46.13.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/d1c8a2a3-18fc-b930-6e8c-5f086e876ea9.gif)

## 対処法

`settins.json`に以下の設定を追記します。

```settings.json
{
  "vim.foldfix": true,
  "vim.normalModeKeyBindingsNonRecursive": [
    {
      "before": ["<C-u>"],
      "after": ["H", "z", "z"]
    },
    {
      "before": ["<C-d>"],
      "after": ["L", "z", "z"]
    }
  ]
}

```

`"vim.foldfix": true,` だけでは `<C-d>` や `<C-u>` でスクロールした際に展開されてしまうため、 `"vim.normalModeKeyBindingsNonRecursive"` も合わせて設定する必要があります。

## 参考

https://arc.net/l/quote/ephkgalk

https://zenn.dev/kenfdev/articles/3637e70b450d56
