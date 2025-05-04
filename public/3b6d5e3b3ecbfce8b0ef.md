---
title: 【JavaScript】fetchのレスポンスのコンテンツタイプが正しいか検証する方法
tags:
  - JavaScript
private: false
updated_at: '2024-02-25T00:00:33+09:00'
id: 3b6d5e3b3ecbfce8b0ef
organization_url_name: null
slide: false
ignorePublish: false
---
以下のようにレスポンスヘッダーの`content-type`を確認することで検証できます。

```javascript
async function fetchSample(request) {
  try {
    const response = await fetch(request);
    
    const contentType = response.headers.get("content-type");
    if (!contentType || !contentType.includes("application/json")) {
      throw new TypeError("JSONではありません。");
    }
    const jsonData = await response.json();
    // ...
    
  } catch (error) {
    console.error("Error:", error);
  }
}
```

https://developer.mozilla.org/ja/docs/Web/API/Fetch_API/Using_Fetch#headers
