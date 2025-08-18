---
title: 【git-spice】ブランチのコミットをsquashする方法
tags:
  - 'git-spice'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
`gs branch squash`コマンドを使用すると、現在のブランチのすべてのコミットを1つのコミットにスカッシュし、上位ブランチ（upstack branches）を自動的にリスタックできます。

## 使用方法

```bash
gs branch squash [flags]
# またはさらに短い省略形
gs b sq [flags]
```

現在のブランチのすべてのコミットを1つにまとめます。

```bash
gs branch squash
```

コマンドを実行するとエディタが開き、スカッシュされたコミットのメッセージを編集できます。その後、上位ブランチが自動的にリスタックされます。

### コミットメッセージを直接指定

`-m`または`--message`フラグを使用して、エディタを開かずにコミットメッセージを直接指定できます。

```bash
gs branch squash -m "機能Aの実装完了"
```

### フックをバイパス

`--no-verify`フラグを使用して、pre-commitおよびcommit-msgフックをバイパスできます。

```bash
gs branch squash --no-verify -m "緊急修正"
```

## 参考

https://abhinav.github.io/git-spice/cli/reference/#gs-branch-squash
