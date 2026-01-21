---
title: 【Zed】ピン留めしたタブを別の行に表示する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-01-21T23:38:17+09:00'
id: e3b6746b706cf9365a1f
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

新しい設定 `show_pinned_tabs_in_separate_row` により、ピン留めタブと通常タブを2行に分けて表示できるようになりました。

**レイアウト:**
- 上段: ピン留めタブ + ナビゲーションボタン
- 下段: 通常タブ(作業中のタブ)

**動的表示:**
- ピン留めタブと通常タブが両方存在する場合のみ2行表示
- どちらか一方のみの場合は1行表示

### Settings UIから設定

1. 設定を開く (Cmd+,)
2. Editor セクションを選択
3. "Pinned Tabs Layout" トグルをオンにする

### settings.jsonで設定

```json
{
  "tab_bar": {
    "show_pinned_tabs_in_separate_row": true
  }
}
```

## 参考

https://github.com/zed-industries/zed/pull/46573
