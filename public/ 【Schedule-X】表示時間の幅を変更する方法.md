---
title: 【Schedule-X】表示時間の幅を変更する方法
tags:
  - Schedule-X
private: false
updated_at: '2026-03-03T23:47:21+09:00'
id: 11ce15a42fecae78e4f6
organization_url_name: null
slide: false
ignorePublish: false
---
## 変更方法

週表示（week grids）と日表示（day grids）の時間範囲を`dayBoundaries`オプションで変更できます。

### 基本的な使い方

```javascript
import { createCalendar } from '@schedule-x/calendar'

const calendar = createCalendar({
  dayBoundaries: {
    start: '08:00',
    end: '18:00'
  }
})
```

### パラメータ

- **start**: グリッドの開始時刻
- **end**: グリッドの終了時刻

**重要**: フルアワー（`HH:00`）のみ指定可能です。`01:30`のような半端な時刻は指定できません。

### ハイブリッドデイ設定

日をまたいだ設定も可能です。
例えば、午前6時から翌日午前3時まで表示する場合

```javascript
const calendar = createCalendar({
  dayBoundaries: {
    start: '06:00',
    end: '03:00' // 翌日の午前3時まで
  }
})
```

## 参考

https://schedule-x.dev/docs/calendar/configuration
