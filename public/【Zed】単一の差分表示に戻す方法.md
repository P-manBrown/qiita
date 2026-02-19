---
title: 【Zed】単一の差分表示に戻す方法
tags:
  - ZedEditor
private: false
updated_at: '2026-02-19T20:34:28+09:00'
id: 434eb530390be58374de
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`settings.json`に以下を追記するとGitの差分表示をスプリットから元に戻せます。

```json
{
  "diff_view_style": "unified",
}
```

- 設定前
![screen-shot-859.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/bcf1443f-4f44-49d3-8d52-8fe89351c315.png)

- 設定後
![screen-shot-858.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/e233d747-4a5f-43f9-8d37-582326f4bf95.png)

## 参考

https://zed.dev/blog/split-diffs
