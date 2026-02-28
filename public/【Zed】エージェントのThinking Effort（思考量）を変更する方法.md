---
title: 【Zed】エージェントのThinking Effort（思考量）を変更する方法
tags:
  - ZedEditor
private: false
updated_at: '2026-02-27T23:56:26+09:00'
id: a124db5585f2b84d7fa5
organization_url_name: null
slide: false
ignorePublish: false
---
## 概要

ZedのAIエージェント機能に「**Thinking Effort（思考量）選択UI**」が正式リリースされました。

## 何が変わったか

これまで `cloud-thinking-effort` というフィーチャーフラグで隠されていた機能が、フラグなしで一般利用可能になりました。

**Zed provider（Zed公式のAIプロバイダー）** を使用している場合、対応モデルに対してAIの思考量（thinking effort）をUIから直接コントロールできるようになります。

## Thinking Effortとは

「拡張思考（Extended Thinking）」に対応したモデルは、回答前により深く推論するかどうかを調整できます。思考量を上げると精度が高まる一方、レスポンスが遅くなる・コストが増えるトレードオフがあります。

| 設定   | 特徴                             |
| ------ | -------------------------------- |
| Low    | 速い・コスト低・簡単なタスク向け |
| Medium | バランス型                       |
| High   | 精度重視・複雑な問題向け         |

## 利用条件

- Zed providerを使用していること（OpenAIやAnthropicの直接APIキー設定では対象外の可能性あり）
- 対応モデル（拡張思考をサポートするモデル）を選択していること

## 参考

https://github.com/zed-industries/zed/pull/49274
