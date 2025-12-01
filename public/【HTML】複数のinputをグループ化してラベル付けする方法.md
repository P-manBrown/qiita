---
title: 【HTML】複数のinputをグループ化してラベル付けする方法
tags:
  - HTML
private: false
updated_at: '2025-12-01T23:55:42+09:00'
id: da6efde84068bb495888
organization_url_name: null
slide: false
ignorePublish: false
---
## fieldsetとlegendを使用

複数の入力欄をグループ化する場合は、`<fieldset>`と`<legend>`を使用するのが適切です。

```html
<fieldset>
  <legend>Range</legend>
  <label for="min">Min</label>
  <input id="min" name="min" />

  <label for="max">Max</label>
  <input id="max" name="max" />
</fieldset>
```

## アクセシビリティを考慮した代替方法

### 方法1: aria-label属性を使用

```html
Range:
<input aria-label="Range start" />
<input aria-label="Range end" />
```

各入力欄に明確な説明を提供できます。

### 方法2: 非表示のlabelタグを使用

```html
<label for="start">Range start</label>
<input type="text" id="start" />

<label for="end" class="hidden">Range end</label>
<input type="text" id="end" />
```

`.hidden`クラスはスクリーンリーダーのみが読み取れるようにします。

### 方法3: aria-labelledby属性を使用

```html
<label id="lblRange">Range</label>
<input type="text" id="start" aria-labelledby="lblRange" />
<input type="text" id="end" aria-labelledby="lblRange" />
```

複数の入力欄が同じラベルを参照します。
