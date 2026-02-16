---
title: 【KeyboardMaestro】Conflict Paletteの透明度を数値で設定する方法
tags:
  - keyboardmaestro
private: false
updated_at: '2026-02-16T23:39:54+09:00'
id: 424068ee4f63e10e09b4
organization_url_name: null
slide: false
ignorePublish: false
---
## 現在の設定を確認

```bash
defaults read com.stairways.keyboardmaestro.engine ConflictMacroPaletteStyle
```

例：

```bash
$ defaults read com.stairways.keyboardmaestro.engine ConflictMacroPaletteStyle
{
    Columns = 2;
    Opacity = 75;
    Size = 15;
    Theme = Custo
    UseDefaultInstead = 0;
    UseTitle = 0;
 
```

## 透明度の変更

```bash
defaults write com.stairways.keyboardmaestro.engine ConflictMacroPaletteStyle -dict-add Opacity -int [数値]
```

例：

```bash
# 完全に不透明
defaults write com.stairways.keyboardmaestro.engine ConflictMacroPaletteStyle -dict-add Opacity -int 100

# 80%の不透明度
defaults write com.stairways.keyboardmaestro.engine ConflictMacroPaletteStyle -dict-add Opacity -int 80

# 半透明
defaults write com.stairways.keyboardmaestro.engine ConflictMacroPaletteStyle -dict-add Opacity -int 50
```

## 変更の確認

```bash
defaults read com.stairways.keyboardmaestro.engine ConflictMacroPaletteStyle
```

例：

```bash
$ defaults read com.stairways.keyboardmaestro.engine ConflictMacroPaletteStyle
{
    Columns = 2;
    Opacity = 80;
    Size = 15;
    Theme = Custom;
    UseDefaultInstead = 0;
    UseTitle = 0;
}
```
