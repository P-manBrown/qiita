---
title: 【Zed】Biomeを使用できるようにする方法
tags:
  - ZedEditor
  - Biome
private: false
updated_at: '2026-03-12T20:05:40+09:00'
id: 77da8eb81846c14446fc
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

**Biome** は Rust 製の高速なコードフォーマッター・リンターです。Zed エディタに統合することで、JavaScript、TypeScript、JSON などのコードを自動的にフォーマット・チェックできます。

## 拡張機能をインストール

1. Zed で `zed: extensions` をコマンドパレットから実行
2. 「Biome」を検索してインストール

**重要**: v0.2.0 以降は **Biome v2** のみ対応です。Biome v1.x を使用する場合は v0.1.5 をインストールしてください。

### Biome バイナリの自動検出

拡張機能は以下の順序で Biome を探します。

1. Zed 設定で指定したパス
2. プロジェクトの `package.json` にローカルインストールされたもの
3. システムの PATH
4. 上記が見つからない場合は npm で自動インストール

## 基本設定

### Biome 設定ファイルを作成

プロジェクトルートに `biome.json` を作成します。

```json
{
  "$schema": "https://biomejs.dev/schemas/2.3.11/schema.json",
  "formatter": {
    "enabled": true,
    "indentStyle": "space",
    "indentSize": 2,
    "lineWidth": 80
  },
  "linter": {
    "enabled": true,
    "rules": {
      "recommended": true
    }
  }
}
```

### Zed の settings.json を設定

**言語ごとに設定することが推奨されます**（グローバル設定は非推奨）。

```json
{
  "languages": {
    "JavaScript": {
      "formatter": { "language_server": { "name": "biome" } },
      "code_actions_on_format": {
        "source.fixAll.biome": true,
        "source.organizeImports.biome": true
      }
    },
    "TypeScript": {
      "formatter": { "language_server": { "name": "biome" } },
      "code_actions_on_format": {
        "source.fixAll.biome": true,
        "source.organizeImports.biome": true
      }
    },
    "JSX": {
      "formatter": { "language_server": { "name": "biome" } }
    },
    "TSX": {
      "formatter": { "language_server": { "name": "biome" } }
    },
    "JSON": {
      "formatter": { "language_server": { "name": "biome" } }
    }
  }
}
```

## よく使う設定

### biome.json のカスタムパスを指定

```json
{
  "lsp": {
    "biome": {
      "settings": {
        "config_path": "config/biome.json"
      }
    }
  }
}
```

### biome.json がある場合のみ有効化

```json
{
  "lsp": {
    "biome": {
      "settings": {
        "require_config_file": true
      }
    }
  }
}
```

### Biome のルールをエディタで上書き

```json
{
  "lsp": {
    "biome": {
      "settings": {
        "inline_config": {
          "linter": {
            "rules": {
              "suspicious": {
                "noConsole": "off"
              }
            }
          }
        }
      }
    }
  }
}
```

## 対応言語

- JavaScript、TypeScript、JSX、TSX
- JSON、JSONC
- Vue.js、Astro、Svelte
- CSS

## 参考資料

https://biomejs.dev/reference/zed/

https://github.com/biomejs/biome-zed

https://zed.dev/docs/languages/biome
