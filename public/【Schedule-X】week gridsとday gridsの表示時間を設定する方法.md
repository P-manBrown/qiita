---
title: 【Schedule-X】week gridsとday gridsの表示時間を設定する方法
tags:
  - Schedule-X
private: false
updated_at: '2026-02-05T20:27:09+09:00'
id: d69b485c1d11703faa3c
organization_url_name: null
slide: false
ignorePublish: false
---
## 表示時間の設定方法

週表示（week grids）と日表示（day grids）の時間範囲は、`dayBoundaries`オプションで設定します。

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
