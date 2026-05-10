---
title: 【Mac】特定の日時にスリープを解除する方法
tags:
  - Mac
  - shell
  - pmset
private: false
updated_at: '2026-05-10T22:06:15+09:00'
id: 178fc89aff27337794bb
organization_url_name: null
slide: false
ignorePublish: false
---

## はじめに

Macには `pmset` というコマンドがあり、電源管理に関するさまざまな設定をターミナルから行えます。この記事では `pmset schedule` を使って特定の日時にスリープを解除する方法と、`pmset repeat` との組み合わせについて説明します。

## pmset schedule で特定の日時にスリープを解除する

`pmset schedule` を使うと、**一度だけ**特定の日時にスリープの解除などをするスケジュールを設定できます。

### 基本的な書き方

```bash
sudo pmset schedule wake "MM/dd/yy HH:mm:ss"
```

`wake` の部分には以下のイベント種別を指定できます。

| イベント | 説明 |
|---|---|
| `wake` | スリープを解除する |
| `poweron` | 電源を入れる |
| `wakeorpoweron` | スリープ解除または電源オン |
| `sleep` | スリープ状態にする |
| `shutdown` | シャットダウンする |

### 使用例

2026年12月10日 の 8:00 にスリープを解除する場合は以下のように実行します。

```bash
sudo pmset schedule wake "12/10/26 08:00:00"
```

### スケジュールの確認

設定したスケジュールは `-g sched` オプションで確認できます。

```bash
pmset -g sched
```

実行例：

```
Scheduled power events:
 [0] [wake] [12/10/26 08:00:00]
```

### スケジュールのキャンセル

設定したスケジュールをキャンセルするには `cancel` を使います。

```bash
sudo pmset schedule cancel wake "12/25/25 08:00:00"
```

すべてのスケジュールをまとめてキャンセルする場合は `cancelall` を使います。

```bash
sudo pmset schedule cancelall
```

## pmset repeat で繰り返しのスリープ解除を設定する

`pmset repeat` を使うと、曜日を指定して**毎週繰り返し**スリープを解除できます。

### 基本的な書き方

```bash
sudo pmset repeat wake 曜日 "HH:mm:ss"
```

曜日は以下の文字で指定します。

| 文字 | 曜日 |
|---|---|
| M | 月曜日 |
| T | 火曜日 |
| W | 水曜日 |
| R | 木曜日 |
| F | 金曜日 |
| S | 土曜日 |
| U | 日曜日 |

### 使用例

平日（月〜金）の毎朝 8:30 にスリープを解除する場合は以下のように実行します。

```bash
sudo pmset repeat wake MTWRF 08:30:00
```

### pmset repeat の制限

`pmset repeat` では**複数の異なる時刻を設定することができません**。たとえば「毎日 8:00と 9:00」のような設定は、`pmset repeat` では実現できません。


## scheduleとrepeatの併用

`pmset schedule` と `pmset repeat` は**同時に使うことができます**。たとえば以下のような組み合わせが可能です。

- `pmset repeat` で平日の毎朝 8:30 に起動するよう設定
- `pmset schedule` で休暇明けの特定日（例：1月6日 7:00）だけ早めに起動するよう追加設定

```bash
# 平日の毎朝 8:30 に繰り返し起動
sudo pmset repeat wake MTWRF 08:30:00

# 1月6日だけ 7:00 に起動（一度限り）
sudo pmset schedule wake "01/06/26 07:00:00"
```

## 参考

https://ss64.com/mac/pmset.html
