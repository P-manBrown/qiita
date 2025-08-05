---
title: 【TailwindCSS】 Functional Utilities
tags:
  - tailwindcss
private: false
updated_at: '2025-08-05T23:26:08+09:00'
id: 136c39c4b2b8f1fc939e
organization_url_name: null
slide: false
ignorePublish: false
---
## Functional Utilitiesとは

Functional Utilitiesは、引数を受け取って動的にCSSを生成できるカスタムユーティリティクラスです。通常のTailwindユーティリティが固定値（例：`text-lg`、`p-4`）を持つのに対し、Functional Utilitiesは値をパラメータとして受け取ることができます。

```css
/* 従来の固定ユーティリティ */
.text-lg { font-size: 1.125rem; }

/* 機能的ユーティリティ */
@utility tab-* {
  tab-size: --value(integer);
}
/* tab-1, tab-2, tab-100 など動的に生成 */
```

## 基本的な実装方法

アスタリスク（`*`）を使用することで、動的な値を受け取ることができます。

```css
@utility tab-* {
  tab-size: --value(--tab-size-*);
}
```

## `--value()`関数の詳細

`--value()`関数は、ユーティリティの値を解決するための特別な関数です。複数の解決方法をサポートしています。

### テーマキーからの値解決

テーマで定義された値を参照できます。

```css
@theme {
  --tab-size-2: 2;
  --tab-size-4: 4;
  --tab-size-github: 8;
  --tab-size-large: 12;
}

@utility tab-* {
  tab-size: --value(--tab-size-*);
}
```

**使用例：**
```html
<div class="tab-2">2文字のタブサイズ</div>
<div class="tab-github">8文字のタブサイズ</div>
<div class="tab-large">12文字のタブサイズ</div>
```

### 直接値の解決

データ型を指定して、直接値を受け取ることができます。

```css
@utility tab-* {
  tab-size: --value(integer);
}
```

**使用例：**
```html
<div class="tab-1">1文字のタブサイズ</div>
<div class="tab-76">76文字のタブサイズ</div>
<div class="tab-999">999文字のタブサイズ</div>
```

**サポートされるデータ型：**
- `integer`: 整数
- `length`: 長さ（px、rem、emなど）
- `percentage`: パーセンテージ
- `color`: カラー値
- その他のCSS数値型

### リテラル値のサポート

特定の文字列値のみを許可することができます。

```css
@utility tab-* {
  tab-size: --value("inherit", "initial", "unset", "revert");
}
```

**使用例：**
```html
<div class="tab-inherit">継承されたタブサイズ</div>
<div class="tab-initial">初期値のタブサイズ</div>
<div class="tab-unset">未設定のタブサイズ</div>
```

### 任意の値のサポート

角括弧記法での任意の値をサポートします。

```css
@utility tab-* {
  tab-size: --value([integer]);
}
```

**使用例：**
```html
<div class="tab-[1]">1文字のタブサイズ</div>
<div class="tab-[8]">8文字のタブサイズ</div>
<div class="tab-[2.5rem]">2.5remのタブサイズ</div>
```

任意の型を許可する場合は`--value([*])`を使用します。

### 複数の値解決パターンの組み合わせ

一つのユーティリティで複数の値解決方法を組み合わせることができます。Tailwindは上から順に評価し、解決できない宣言は出力から除外されます。

```css
@theme {
  --tab-size-github: 8;
  --tab-size-small: 2;
}

@utility tab-* {
  tab-size: --value([integer]);          /* 任意の値: tab-[4] */
  tab-size: --value(integer);            /* ベア値: tab-4 */
  tab-size: --value(--tab-size-*);       /* テーマ値: tab-github */
}
```

この設定により、以下のすべてのパターンが使用可能になります：

```html
<div class="tab-[4]">任意の値</div>
<div class="tab-4">ベア値</div>
<div class="tab-github">テーマ値</div>
<div class="tab-small">テーマ値</div>
```

### 負の値のサポート

正の値と負の値を別々に定義することで、負の値をサポートできます。

```css
@utility inset-* {
  inset: --spacing(--value(integer));
  inset: --value([percentage], [length]);
}

@utility -inset-* {
  inset: --spacing(--value(integer) * -1);
  inset: calc(--value([percentage], [length]) * -1);
}
```

**使用例：**
```html
<div class="inset-4">正の値</div>
<div class="-inset-4">負の値</div>
<div class="inset-[10%]">正のパーセンテージ</div>
<div class="-inset-[10%]">負のパーセンテージ</div>
```

### 分数値の処理

CSS `ratio`データ型を使用して分数を処理できます。

```css
@utility aspect-* {
  aspect-ratio: --value(--aspect-ratio-*, ratio, [ratio]);
}
```

**使用例：**
```html
<div class="aspect-16/9">16:9のアスペクト比</div>
<div class="aspect-3/4">3:4のアスペクト比</div>
<div class="aspect-[7/9]">カスタムアスペクト比</div>
```

## 実用的な応用例

### 透明度ユーティリティ

```css
@theme {
  --opacity-10: 0.1;
  --opacity-50: 0.5;
  --opacity-75: 0.75;
}

@utility opacity-* {
  opacity: --value([percentage]);           /* opacity-[50%] */
  opacity: calc(--value(integer) * 1%);     /* opacity-50 → 50% */
  opacity: --value(--opacity-*);            /* opacity-50 → 0.5 */
}
```

### グリッドユーティリティ

```css
@utility grid-cols-* {
  grid-template-columns: repeat(--value(integer), minmax(0, 1fr));
  grid-template-columns: --value([*]);
}
```

**使用例：**
```html
<div class="grid grid-cols-3">3カラムグリッド</div>
<div class="grid grid-cols-[200px_1fr_100px]">カスタムグリッド</div>
```

### カスタムスペーシング

```css
@theme {
  --spacing-xs: 0.25rem;
  --spacing-sm: 0.5rem;
  --spacing-md: 1rem;
  --spacing-lg: 2rem;
}

@utility gap-* {
  gap: --value(--spacing-*, [length]);
  gap: --spacing(--value(integer));
}
```

## 参考

https://tailwindcss.com/docs/adding-custom-styles#functional-utilities
