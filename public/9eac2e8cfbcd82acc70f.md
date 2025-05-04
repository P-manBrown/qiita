---
title: 【React】内容に合わせて高さが変わるtextarea
tags:
  - React
private: false
updated_at: '2023-12-04T00:09:00+09:00'
id: 9eac2e8cfbcd82acc70f
organization_url_name: null
slide: false
ignorePublish: false
---
以下のように記述することで内容に合わせてtextareaの高さを自動で変更できます。

```tsx:Textarea.tsx

export default function TextArea() {
  return (
    <textarea
        onChange={(ev) => {
          ev.currentTarget.style.height = 'auto'
          ev.currentTarget.style.height = `${ev.currentTarget.scrollHeight}px`
        }}
    />
  )
}

```
