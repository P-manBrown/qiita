---
title: 【Serena】編集を禁止する方法
tags:
  - Serena
private: false
updated_at: '2025-12-09T23:59:10+09:00'
id: fbd2fedf2b9d9f528a65
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

プロジェクトディレクトリ内の`.serena/project.yml`ファイルの`read_only`を`true`に変更します。

```yaml
read_only: true
```

この設定により、以下の効果が得られます。

- **すべての編集ツールが自動的に無効化**
- **ファイルの変更を防止**
- **分析・探索機能はすべて利用可能**

## 参考

https://github.com/oraios/serena/blob/main/README.md#shell-execution-and-editing-tools
