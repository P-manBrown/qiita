---
title: 【Zed】エラーメッセージをインラインで表示する方法
tags:
  - ZedEditor
private: false
updated_at: '2025-06-29T23:35:43+09:00'
id: fc5a5fd6ee6837e0891a
organization_url_name: null
slide: false
ignorePublish: false
---
## 表示方法

エラーメッセージをインラインで表示するには`settings.json`に以下を追記します。

```jsonc
{
	"diagnostics": {
    "inline": {
      "enabled": true
    }
  },
}

```

画像のようにエラーメッセージがインラインで表示されるようになります。

![screen-shot-407.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/45272928-0784-459c-afe3-b12526fa9034.png)

## 表示の設定

```jsonc
{
	"diagnostics": {
    "inline": {
      "enabled": true,
      // 最後の診断更新から一定期間経過するまで、診断更新を遅延
      "update_debounce_ms": 150,
      // ソース行の末尾と診断の開始の間に padding を設定
      "padding": 4,
      // 指定された列でエラーメッセージを水平方向に揃える
      "min_column": 0,
      // 警告とエラーの診断情報のみを表示
      "max_severity": "warning"
    }
  },
}

```

## 参考

https://zed.dev/docs/configuring-zed#inline-diagnostics
