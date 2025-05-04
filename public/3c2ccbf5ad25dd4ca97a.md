---
title: 【Mac】コマンドでブラウザで特定のURLを開く方法
tags:
  - Mac
  - 初学者
private: false
updated_at: '2022-10-01T19:50:02+09:00'
id: 3c2ccbf5ad25dd4ca97a
organization_url_name: null
slide: false
ignorePublish: false
---
## 方法
以下のように実行すると特定のURLを指定したブラウザで開けます。

```zsh
open -a 'ブラウザ名.app' <URL>
```
- ChoromeでURLを開く場合
```zsh
open -a 'Google Chrome.app' <URL>
```
- SafariでURLを開く場合
```zsh
open -a 'Safari.app' <URL>
```

## 具体例
- Chromeで https://github.com/ を開く
```zsh
open -a 'Google Chrome.app' "https://github.com/"
```

- Safariで https://qiita.com/ を開く
```zsh
open -a 'Safari.app' "https://qiita.com/"
```
