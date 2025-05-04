---
title: 【VSCode】固定したタブを別の行に表示する方法
tags:
  - VSCode
private: false
updated_at: '2024-06-05T00:12:38+09:00'
id: 4d707f52feb4c3bde3ec
organization_url_name: null
slide: false
ignorePublish: false
---
`workbench.editor.pinnedTabsOnSeparateRow` を有効にすると固定したタブが別の行に表示されます。

![pinned-tabs-on-separate-row.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/73a5c80d-e179-0e32-3386-882feb99618f.gif)

また `window.density.editorTabHeight` を `conpact` に設定することでタブの高さを低くできます。

![editor-tab-height-compact.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/c7fbfbe4-39fc-bfa5-172a-eef361f9aea2.png)

さらに `workbench.editor.wrapTabs` を有効にするとタブが折り返されるようになります。

![tabs-wrap.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/2ea890fb-3b8b-8135-b74d-d68d85810105.gif)
