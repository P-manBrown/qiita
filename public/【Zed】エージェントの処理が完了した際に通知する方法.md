---
title: 【Zed】エージェントの処理が完了した際に通知する方法
tags:
  - ZedEditor
private: false
updated_at: '2025-07-02T23:27:27+09:00'
id: 5b46c8fc8c6c5cc21e6c
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`settings.json`に以下を追記することで、エージェントの処理が完了した際にZedのウインドーにフォーカスがないと通知音が鳴るようになります。

```jsonc
{
	"agent": {
    "play_sound_when_agent_done": true
  }
}

```

以下を追記するとすべてのスクリーンの右上に通知が表示されるようになります。

```jsonc
}
	"agent": {
    "notify_when_agent_waiting": "all_screens"
	}
}
```

## 参考

https://zed.dev/docs/ai/agent-panel#get-notified
