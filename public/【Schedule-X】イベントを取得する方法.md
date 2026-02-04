---
title: 【Schedule-X】イベントを取得する方法
tags:
  - Schedule-X
private: false
updated_at: '2026-02-04T20:15:05+09:00'
id: 060e34a5da80601009d4
organization_url_name: null
slide: false
ignorePublish: false
---
## fetchEventsコールバックを使用する

`fetchEvents`コールバックは、表示範囲が変更されるたびに自動的に呼び出され、取得したイベントがカレンダーに反映されます。

### 基本的な実装

```typescript
import { createCalendar, viewWeek, viewMonthGrid } from '@schedule-x/calendar'
import '@schedule-x/theme-default/dist/index.css'

const calendar = createCalendar({
  views: [viewWeek, viewMonthGrid],
  callbacks: {
    async fetchEvents(range) {
      const events = await fetch(`/api/events?start=${range.start}&end=${range.end}`)
        .then((res) => res.json())
      return events
    }
  }
})

calendar.render(document.getElementById('calendar'))
```

## 実行タイミング

`fetchEvents`は以下のタイミングで呼び出されます。

- 初回レンダリング時
- 日付ピッカーで日付を選択したとき
- ビューを切り替えたとき

## rangeオブジェクト

`fetchEvents`コールバックに渡される`range`オブジェクトには以下のプロパティが含まれます。

- `range.start`: 表示範囲の開始日時
- `range.end`: 表示範囲の終了日時

## イベントの自動反映

`fetchEvents`から返されたイベントは、自動的に`$app.calendarEvents.list.value`に変換・設定されるため、手動でカレンダーを更新する必要がありません。

## 参考

https://schedule-x.dev/docs/calendar/configuration
