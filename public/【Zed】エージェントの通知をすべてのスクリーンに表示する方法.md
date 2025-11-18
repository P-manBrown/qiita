---
title: 【Zed】エージェントの通知をすべてのスクリーンに表示する方法
tags:
  - 'ZedEditor'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`settings.json`に以下を追記するとすべてのスクリーンの右上に通知が表示されるようになります。

```jsonc
}
  "agent": {
    "notify_when_agent_waiting": "all_screens"
  }
}
```

## 参考

https://zed.dev/docs/ai/agent-panel#get-notified
