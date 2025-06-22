---
title: 【Mac】コマンドでQRコードを生成する方法
tags:
  - Mac
private: false
updated_at: '2025-06-22T23:42:25+09:00'
id: f9b74bbcb92f302627e0
organization_url_name: null
slide: false
ignorePublish: false
---
## qrencodeをインストール

以下のコマンドで`qrencode`をインストールする。

```terminal
brew install qrencode
```

## qrencodeの使い方

文字列をQRコードに変換してファイルに保存する。

```terminal
qrencode -o path/to/output_file.png 'string'
```

入力ファイルをQRコードに変換し、ファイルに保存する。

```terminal
qrencode -o path/to/output_file.png -r path/to/input_file
```

文字列をQRコードに変換してターミナルに表示する。

```terminal
qrencode -t ansiutf8 'string'
```

パイプからの入力をQRコードに変換してターミナルに表示する。

```terminal
echo 'string' | qrencode -t ansiutf8
```
