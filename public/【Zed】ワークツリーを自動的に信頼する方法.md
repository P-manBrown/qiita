---
title: 【Zed】ワークツリーを自動的に信頼する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-01-08T23:54:41+09:00'
id: c391e2447df505dbb4d1
organization_url_name: null
slide: false
ignorePublish: false
---
## 制限モードとは

制限モードでは、Zedは以下の操作を実行前に許可を求めます。

- プロジェクトの`.zed/settings.json`の解析と適用
- 言語サーバーのダウンロードと起動
- MCPサーバーのインストールと起動

## すべてのワークツリーを自動的に信頼する方法

Zedの設定ファイル（`settings.json`）に以下を追加します。

```json
{
  "session": {
    "trust_all_worktrees": true
  }
}
```

## 注意事項

この設定を有効にすると、Zedは新しいワークツリーからのコード実行を確認なしで許可します。以下のリスクがあることを理解した上で使用してください。

- 悪意のあるリポジトリをクローンした場合、任意のコードが自動実行される可能性がある
- セキュリティの確認ステップがスキップされる

この設定は、サンドボックス環境や信頼できるプロジェクトのみを扱う場合に適しています。通常の開発環境では、手動で信頼するワークツリーを選択することを推奨します。

## 参考

https://zed.dev/blog/secure-by-default



https://zed.dev/docs/worktree-trust
