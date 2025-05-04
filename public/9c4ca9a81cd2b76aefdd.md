---
title: 【Fish】viキーバインディングを使用する方法
tags:
  - fish
private: false
updated_at: '2025-03-23T23:34:03+09:00'
id: 9c4ca9a81cd2b76aefdd
organization_url_name: null
slide: false
ignorePublish: false
---
## viキーバインディングの有効化

Fishでviキーバインディンを使用可能にするには、`~/.config/fish/config.fish`に以下の記述を追記します。

```shell:~/.config/fish/config.fish 
set -g fish_key_bindings fish_vi_key_bindings
```

https://fishshell.com/docs/current/cmds/fish_vi_key_bindings.html

## 入力モードによってカーソルを変更する

`~/.config/fish/config.fish`に以下を追記することで入力モードによってカーソルが変更されるようになります。

```config.fish
set -g fish_cursor_default block

set -g fish_cursor_insert line

set -g fish_cursor_replace_one underscore
set -g fish_cursor_replace underscore

set -g fish_cursor_external line

set -g fish_cursor_visual block

set -g fish_vi_force_cursor true

```

![画面収録 2025-01-07 23.59.03.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/422d54c6-7114-352e-9cec-268f7ace607f.gif)

https://fishshell.com/docs/current/interactive.html#autosuggestions

## ヤンクしたテキストをクリップボードに保存する

`~/.config/fish/config.fish`に以下のように記述するとviモードでヤンクしたテキストがクリップボードに保存されるようになります。

```shell:config.fish
bind yy fish_clipboard_copy
bind Y fish_clipboard_copy
bind p fish_clipboard_paste
```

https://github.com/fish-shell/fish-shell/issues/4028#issuecomment-1791599167

https://fishshell.com/docs/current/cmds/fish_clipboard_copy.html
