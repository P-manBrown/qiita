---
title: 【Mac】Spotlightのインデックス作成を無効化する方法
tags:
  - Mac
private: false
updated_at: '2025-05-19T23:01:16+09:00'
id: 33f58e3046f2a787ab47
organization_url_name: null
slide: false
ignorePublish: false
---

## 無効化

以下のコマンドを実行するとSpotlightのインデックス作成を無効化できます。

```terminal
sudo mdutil -a -i off
```

次のように無効化できたか確認できます。

```terminal
$ sudo mdutil -a -s
/:
        Indexing disabled.
/System/Volumes/Data:
        Indexing disabled.
/System/Volumes/Preboot:
        Indexing disabled.
```

## 有効化

再度有効化するには以下のコマンドを実行します。

```terminal
sudo mdutil -a -i on
```

```terminal
$ sudo mdutil -a -s
Password:
/:
        Indexing enabled.
/System/Volumes/Data:
        Indexing enabled.
/System/Volumes/Preboot:
        Indexing enabled.
```
