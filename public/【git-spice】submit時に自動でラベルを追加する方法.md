---
title: 【git-spice】submit時に自動でラベルを追加する方法
tags:
  - git-spice
private: false
updated_at: '2026-01-20T23:57:31+09:00'
id: 4d8c6da368f74b4238a6
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`.git/config`または`~/.gitconfig`に以下を追加します。

```toml
[spice.submit]
    label = bug,needs-review
```

カンマ区切りで複数のラベルを指定できます。

## 使い方

### 基本的な使用

設定後、通常通り`gs branch submit`を実行するだけで、設定したラベルが自動的に付与されます。

```bash
gs branch submit
```

### コマンドラインでの追加指定

`-l`/`--label`フラグを使用すると、設定ファイルのラベルに加えて、追加のラベルを指定できます。

```bash
gs branch submit -l urgent -l hotfix
```

この場合、`bug`、`needs-review`、`urgent`、`hotfix`の4つのラベルが付与されます。

