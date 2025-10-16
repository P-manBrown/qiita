---
title: 【Zed】Snippetの表示位置を変更する方法
tags:
  - ZedEditor
private: false
updated_at: '2025-06-26T23:08:12+09:00'
id: 2843c3f15710e0742526
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

Snippetの表示位置は`settings.json`の`snippet_sort_order`で設定できます。

- 一番上に表示

```json
{
  "snippet_sort_order": "top",
}
```

- 他の候補と同等の優先順位で表示

```json
{
  "snippet_sort_order": "inline",
}
```

- 一番下に表示

```json
{
  "snippet_sort_order": "bottom",
}
```

## 参考

https://zed.dev/docs/configuring-zed?highlight=snippet%20sort#snippet-sort-order
