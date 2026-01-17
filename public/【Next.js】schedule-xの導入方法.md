---
title: 【Next.js】schedule-xの導入方法
tags:
  - Next.js
private: false
updated_at: '2026-01-17T23:31:35+09:00'
id: c879d3ba0486db207ecd
organization_url_name: null
slide: false
ignorePublish: false
---
## 必要なパッケージのインストール

まず、必要なパッケージをインストールします。

```bash
npm install @schedule-x/react @schedule-x/calendar @schedule-x/theme-default @schedule-x/events-service temporal-polyfill
```

## カレンダーコンポーネントの作成

Next.jsではクライアントコンポーネントとして実装する必要があります。

```tsx
'use client'

import { useNextCalendarApp, ScheduleXCalendar } from '@schedule-x/react'
import {
  createViewDay,
  createViewWeek,
  createViewMonthGrid,
  createViewMonthAgenda,
} from '@schedule-x/calendar'
import { createEventsServicePlugin } from '@schedule-x/events-service'
import { useState } from 'react'
import 'temporal-polyfill/global'
import '@schedule-x/theme-default/dist/index.css'

export default function CalendarApp() {
  const eventsService = useState(() => createEventsServicePlugin())[0]

  const calendar = useNextCalendarApp({
    views: [
      createViewDay(),
      createViewWeek(),
      createViewMonthGrid(),
      createViewMonthAgenda()
    ],
    events: [
      {
        id: '1',
        title: 'サンプルイベント',
        start: Temporal.PlainDate.from('2025-01-20'),
        end: Temporal.PlainDate.from('2025-01-20'),
      },
    ],
    plugins: [eventsService],
    callbacks: {
      onRender: () => {
        eventsService.getAll()
      }
    }
  })

  return (
    <div>
      <ScheduleXCalendar calendarApp={calendar} />
    </div>
  )
}
```

## スタイルの調整

カレンダーのサイズを調整するため、CSSを追加します。
```css
.sx-react-calendar-wrapper {
  width: 1200px;
  max-width: 100vw;
  height: 800px;
  max-height: 90vh;
}
```

## 参考

- [Schedule-X公式ドキュメント](https://schedule-x.dev/docs/frameworks/react)
