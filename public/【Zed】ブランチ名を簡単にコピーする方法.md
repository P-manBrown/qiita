---
title: 【Zed】ブランチ名を簡単にコピーする方法
tags:
  - ZedEditor
private: false
updated_at: '2026-05-08T23:32:03+09:00'
id: 51584a798020d8a358ae
organization_url_name: null
slide: false
ignorePublish: false
---

## はじめに

GitHubのPRレビューやチームへの共有など、現在のブランチ名をコピーしたい場面はよくあります。

Zed v1.1.5 で `git: copy branch name` アクションが追加され、現在チェックアウトしているブランチ名をワンステップでクリップボードにコピーできるようになりました。

## 使い方

### コマンドパレットから実行する

最も簡単な方法は、コマンドパレットを使うことです。

1. `Cmd + Shift + P`（macOS）または `Ctrl + Shift + P`（Linux/Windows）でコマンドパレットを開く
2. `git: copy branch name` と入力して選択する

これだけで、現在のブランチ名がクリップボードにコピーされます。

### キーバインドを設定する

頻繁に使う場合は、キーバインドを登録しておくと便利です。

`keymap.json` に以下を追加することで、任意のキーに割り当てられます。

```json
[
  {
    "context": "Workspace",
    "bindings": {
      "ctrl-shift-b": "git::CopyBranchName"
    }
  }
]
```

キーバインドファイルは、コマンドパレットから `zed: open keymap` と入力することで開けます。

## 内部の仕組み（参考）

このアクションは、Gitパネルがアクティブなリポジトリから現在のブランチ名を取得し、クリップボードに書き込む処理をしています。

```rust
fn copy_branch_name(workspace: &mut Workspace, cx: &mut Context<Workspace>) {
    let Some(panel) = workspace.panel::<GitPanel>(cx) else {
        return;
    };
    let branch_name = panel.update(cx, |panel, cx| {
        let repo = panel.active_repository.as_ref()?;
        let repo = repo.read(cx);
        repo.branch.as_ref().map(|branch| branch.name().to_string())
    });
    if let Some(name) = branch_name {
        cx.write_to_clipboard(ClipboardItem::new_string(name));
    }
}
```

Gitパネルが開いていない状態や、リポジトリが存在しないプロジェクトでは何も起こらない設計になっています。

## 参考

https://github.com/zed-industries/zed/pull/54702

https://zed.dev/releases/stable/1.1.5
