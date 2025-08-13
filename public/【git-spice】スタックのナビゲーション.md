---
title: 【git-spice】スタックのナビゲーション
tags:
  - 'git-spice'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 基本的なナビゲーションコマンド

### 上下移動

git-spiceは、スタック内でのナビゲーションのために以下のコマンドを提供します。

```bash
# 一つ下のブランチに移動
gs down

# 一つ上のブランチに移動（複数ある場合は選択プロンプト）
gs up

# スタックの最下位ブランチに移動（trunkの直上）
gs bottom

# スタックの最上位ブランチに移動（複数ある場合は選択プロンプト）
gs top
```

### ドライランオプション

`-n`フラグを使用することで、実際にチェックアウトせずにターゲットブランチを確認できます。

```bash
# 移動先ブランチを確認のみ（実際には移動しない）
gs up -n
gs down -n
gs top -n
gs bottom -n
```

## インタラクティブなナビゲーション

`gs branch checkout`を引数なしで実行すると、ファジー検索可能なブランチリストが表示され、ツリー状の構造でスタックをナビゲートできます。

```bash
# インタラクティブなブランチ選択
gs branch checkout
# または短縮形
gs bco
```

コマンドを実行すると、以下のような画面が表示されます。

```
                ┏━□ wip/feature-c
              ┏━┻■ feat/feature-b ◀
            ┏━┻□ fix/bug-fix-a
          ┏━┻□ feat/feature-a
        ┏━┻□ fix/bug-fix-b
      ┏━┻□ feat/core-feature
    ┏━┻□ feat/base-implementation
  ┏━┻□ feat/initial-setup
┏━┻□ fix/foundation-fix
main
```

矢印キーで選択し、Enterで決定、検索文字列を入力してファジー検索も可能です。現在選択されているブランチは `◀` で示され、各ブランチの状態が視覚的に表示されます。
