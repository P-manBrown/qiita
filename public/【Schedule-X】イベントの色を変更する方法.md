---
title: 【Schedule-X】イベントの色を変更する方法
tags:
  - Schedule-X
private: false
updated_at: '2026-03-02T22:52:26+09:00'
id: 68d6fb7276869f1c7434
organization_url_name: null
slide: false
ignorePublish: false
---
## 変更方法

イベントに `calendarId` を指定することで色分けが可能です。

### 例

```typescript
import { createCalendar } from '@schedule-x/calendar'
import '@schedule-x/theme-default/dist/index.css'

const calendar = createCalendar({
  calendars: {
    personal: {
      colorName: 'personal',
      lightColors: {
        main: '#f9d71c',
        container: '#fff5aa',
        onContainer: '#594800',
      },
    },
    work: {
      colorName: 'work',
      lightColors: {
        main: '#f91c45',
        container: '#ffd2dc',
        onContainer: '#59000d',
      },
    },
  },
  events: [
    {
      id: '1',
      title: '会議',
      start: Temporal.ZonedDateTime.from('2025-02-08T10:00:00+09:00[Asia/Tokyo]'),
      end: Temporal.ZonedDateTime.from('2025-02-08T11:00:00+09:00[Asia/Tokyo]'),
      calendarId: 'work',
    },
    {
      id: '2',
      title: '買い物',
      start: Temporal.ZonedDateTime.from('2025-02-08T15:00:00+09:00[Asia/Tokyo]'),
      end: Temporal.ZonedDateTime.from('2025-02-08T16:00:00+09:00[Asia/Tokyo]'),
      calendarId: 'personal',
    },
  ],
})

calendar.render(document.getElementById('calendar'))
```

## カラープロパティの説明

各カレンダーには3つのカラープロパティを設定します。

- `main`: イベントのメインカラー
- `container`: イベントの背景色
- `onContainer`: イベント内のテキスト色

## ダークモード対応

ライトモードとダークモードの両方を使用する場合は、`darkColors` も定義します。

```typescript
calendars: {
  work: {
    colorName: 'work',
    lightColors: {
      main: '#f91c45',
      container: '#ffd2dc',
      onContainer: '#59000d',
    },
    darkColors: {
      main: '#ffc0cc',
      onContainer: '#ffdee6',
      container: '#a24258',
    },
  },
}
```

## 注意点

- `colorName` は小文字のみ使用可能(CSS変数として使用されるため)
- イベントに `calendarId` を指定しない場合、デフォルトの色が適用されます
- カレンダー名は任意に設定可能(JavaScriptのオブジェクトキーとして使用できる文字列)
