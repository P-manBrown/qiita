---
title: 【Zed】ターミナルで選択したテキストをAIアシスタントに渡す方法
tags:
  - ZedEditor
private: false
updated_at: '2026-02-15T23:56:49+09:00'
id: 986cb58923ebfc3ea3ca
organization_url_name: null
slide: false
ignorePublish: false
---
## 方法

### コンテキストメニューから追加

1. ターミナルでテキストを選択
2. 右クリック → **"Add to Agent Thread"** を選択
3. Agent Panelに折りたたまれた「Terminal」ブロックとして表示される

### キーボードショートカットで追加

- **macOS**: `Cmd + >`
- **Windows/Linux**: `Ctrl + >`

ターミナルでテキストを選択した状態でこのショートカットを実行すると、即座にAgent Threadに追加されます。

## 特徴

- **折りたたみ表示**: ターミナル出力は「Terminal」という折りたたみ可能なブロックとして表示され、チャット履歴がスッキリ保たれます
- **両方のスレッドタイプに対応**: Claude Code（ACP）スタイルとテキストスレッドの両方で使用可能
- **エディタと同じ操作感**: エディタの選択範囲をコンテキストに追加するのと同じ操作で利用できます

## 参考

https://github.com/zed-industries/zed/pull/47637
