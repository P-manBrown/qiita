---
title: 【git-spice】ブランチを挿入する方法
tags:
  - git-spice
private: false
updated_at: '2025-08-12T22:45:43+09:00'
id: efc1493b32039612054d
organization_url_name: null
slide: false
ignorePublish: false
---
## --insert オプション：ブランチをスタックの途中に挿入

`--insert` オプションを使用すると、新しいブランチを現在のブランチとその上位ブランチの間に挿入できます。

```bash
gs branch create ブランチ名 --insert
```

### 例

元のスタック状態が以下のようになっているとします（Aがチェックアウトされている状態）。

```
     ┌── C
   ┌─┴ B
 ┌─┴ A ◀ (current)
trunk
```

この状態で `gs branch create X --insert` を実行すると

```
       ┌── C
     ┌─┴ B
   ┌─┴ X
 ┌─┴ A
trunk
```

新しいブランチXがAとBの間に挿入されます。

## --below オプション：ブランチをスタックの下に挿入

`--below` オプションは、新しいブランチを現在のブランチの下に挿入します。

```bash
gs branch create ブランチ名 --below
```

### 例

```
     ┌── C
   ┌─┴ B
 ┌─┴ A ◀ (current)
trunk
```

同じ初期状態で `gs branch create X --below` を実行すると

```
      ┌── C
    ┌─┴ B
  ┌─┴ A
┌─┴ X
trunk
```

新しいブランチXがAの下（trunkとAの間）に挿入されます。

## --target オプションとの組み合わせ

`--target` オプションと組み合わせることで、現在のブランチ以外を基準にした挿入も可能です。

### 例

```bash
# ブランチBを基準として、その上に挿入
gs branch create X --insert --target B

# ブランチBを基準として、その下に挿入
gs branch create X --below --target B
```

初期状態

```
     ┌── C
   ┌─┴ B
 ┌─┴ A ◀ (current)
trunk
```

`gs branch create X --insert --target B` の場合

```
      ┌── C
    ┌─┴ X
  ┌─┴ B
┌─┴ A
trunk
```

`gs branch create X --below --target B` の場合

```
      ┌── C
    ┌─┴ B
  ┌─┴ X
┌─┴ A
trunk
```
