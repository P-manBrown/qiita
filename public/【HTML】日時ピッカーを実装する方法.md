---
title: 【HTML】日時ピッカーを実装する方法
tags:
  - HTML
private: false
updated_at: '2025-11-30T21:42:44+09:00'
id: 33d9c9004c94d3cecd6b
organization_url_name: null
slide: false
ignorePublish: false
---
## 日時ピッカーの種類

### 1. 日付ピッカー（date）

年月日を選択するウィジェットを表示します。

```html
<input type="date" name="date" id="date" />
```

### 2. 日時ピッカー（datetime-local）

タイムゾーン情報を含まない日付と時刻を選択できます。

```html
<input type="datetime-local" name="datetime" id="datetime" />
```

### 3. 月ピッカー（month）

年と月を選択するウィジェットです。

```html
<input type="month" name="month" id="month" />
```

### 4. 時刻ピッカー（time）

時刻を選択します。表示は12時間形式でも、返される値は24時間形式です。

```html
<input type="time" name="time" id="time" />
```

### 5. 週ピッカー（week）

週番号と年を選択できます。

```html
<input type="week" name="week" id="week" />
```

## 値の制約

`min`、`max`、`step`属性で値の範囲を制限できます。

```html
<label for="myDate">今年の夏、いつ空いていますか？</label><br />
<input
  type="date"
  name="myDate"
  min="2025-06-01"
  max="2025-08-31"
  step="7"
  id="myDate" />
```

- 2025年6月1日から8月31日までの範囲に制限
- `step="7"`で7日刻みで選択可能

## 例：日付範囲の選択

```html
<form>
  <div>
    <label for="start-date">開始日:</label>
    <input type="date" id="start-date" name="start-date" min="2025-01-01" />
  </div>
  <div>
    <label for="end-date">終了日:</label>
    <input type="date" id="end-date" name="end-date" min="2025-01-01" />
  </div>
</form>
```

## 参考

https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/HTML5_input_types
