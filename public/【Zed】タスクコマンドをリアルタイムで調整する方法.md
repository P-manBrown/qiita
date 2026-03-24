---
title: 【Zed】タスクコマンドをリアルタイムで調整する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-03-25T00:18:08+09:00'
id: a31e525143c9ca071911
organization_url_name: null
slide: false
ignorePublish: false
---
## タスクコマンドをその場で編集する方法

**1. コマンドパレットを開く**

`Cmd+Shift+P`（macOS）または `Ctrl+Shift+P`（Windows/Linux）でコマンドパレットを開き、`task: spawn` を選択します。

**2. タスクモーダルに表示されるタスクを選ぶ**

実行したいタスクにカーソルを合わせます。この時点ではまだ実行しません。

**3. `Tab` キーを押してコマンドを展開する**

`Tab` を押すと、そのタスクの**実際のコマンド文字列**がモーダルの入力欄に展開されます。

```
cargo test --package my_crate tests::my_test -- --nocapture
```

このような形でコマンド全体が表示されます。

**4. コマンドを自由に編集する**

入力欄はそのまま編集可能です。たとえば先頭に環境変数を追加できます。

```
RUST_BACKTRACE=1 cargo test --package my_crate tests::my_test -- --nocapture
```

**5. `Alt+Enter` で実行する（Oneshot タスク）**

編集が終わったら `Alt+Enter` を押します。これで入力欄に現在あるコマンドがそのまま実行されます。

この「Oneshot タスク」機能により、定義済みタスクを変形させて一度だけ実行することができます。

Oneshot タスクのドキュメント：

https://zed.dev/docs/tasks?highlight=one-off#oneshot-tasks

## 参考

https://zed.dev/blog/hidden-gems-part-2#adjust-task-commands-on-the-fly
