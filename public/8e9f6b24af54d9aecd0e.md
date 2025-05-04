---
title: >-
  【Homebrew】Warning: Skipping FORMULA: most recent version 0.0.0 not installed
  解消法
tags:
  - homebrew
private: false
updated_at: '2022-10-17T15:41:42+09:00'
id: 8e9f6b24af54d9aecd0e
organization_url_name: null
slide: false
ignorePublish: false
---
## 状況

`brew cleanup`を実行した際に以下のような警告が表示されました。  

```zsh
$ brew cleanup
Removing: /opt/homebrew/Cellar/libomp/14.0.6... (7 files, 1.6MB)
Warning: Skipping openssl@3: most recent version 3.0.5 not installed
Removing: /opt/homebrew/Cellar/python@3.10/3.10.7... (3,114 files, 57.2MB)
Removing: /Users/username/Library/Caches/Homebrew/python@3.10--3.10.7... (14.7MB)
Removing: /opt/homebrew/Cellar/unbound/1.16.3... (58 files, 5.7MB)
Removing: /Users/username/Library/Caches/Homebrew/unbound--1.16.3... (2.8MB)
Pruned 0 symbolic links and 2 directories from /opt/homebrew
==> This operation has freed approximately 81.9MB of disk space.
```

`openssl@3`の更新を試みましたが以下のとおり出力され変化はありませんでした。  

```zsh
$ brew update

$ brew upgrade openssl@3
Warning: openssl@3 3.0.6 already installed

$ brew cleanup
Warning: Skipping openssl@3: most recent version 3.0.5 not installed
```

また`brew outdated`を実行しても何も表示されませんでした。  

## 解決した方法

以下のコマンドを入力し、`openssl@3`を再インストールしたところ解消されました。  

```zsh
$ brew reinstall openssl@3
==> Downloading https://ghcr.io/v2/homebrew/core/openssl/3/manifests/3.0.5
######################################################################## 100.0$
==> Downloading https://ghcr.io/v2/homebrew/core/openssl/3/blobs/sha256:d0cc00946bd11f14e1e0f94ce7c2
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:d0cc00946bd11f1
######################################################################## 100.0$
==> Reinstalling openssl@3
==> Pouring openssl@3--3.0.5.arm64_monterey.bottle.tar.gz
==> Caveats
A CA file has been bootstrapped using certificates from the system
keychain. To add additional certificates, place .pem files in
  /opt/homebrew/etc/openssl@3/certs

and run
  /opt/homebrew/opt/openssl@3/bin/c_rehash

openssl@3 is keg-only, which means it was not symlinked into /opt/homebrew,
because macOS provides LibreSSL.

If you need to have openssl@3 first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/openssl@3/bin:$PATH"' >> ~/.zshrc

For compilers to find openssl@3 you may need to set:
  export LDFLAGS="-L/opt/homebrew/opt/openssl@3/lib"
  export CPPFLAGS="-I/opt/homebrew/opt/openssl@3/include"

For pkg-config to find openssl@3 you may need to set:
  export PKG_CONFIG_PATH="/opt/homebrew/opt/openssl@3/lib/pkgconfig"

==> Summary
🍺  /opt/homebrew/Cellar/openssl@3/3.0.5: 6,444 files, 27.9MB
==> Running `brew cleanup openssl@3`...
Disable this behaviour by setting HOMEBREW_NO_INSTALL_CLEANUP.
Hide these hints with HOMEBREW_NO_ENV_HINTS (see `man brew`).

$ brew cleanup
Pruned 0 symbolic links and 2 directories from /opt/homebrew

```

* 参考ページ  

https://github.com/Homebrew/discussions/discussions/3500

## 解決しなかった方法

参考ページ記載の`brew unlink FORMULA` `brew link FORMULA`では解消しませんでした。

```zsh
$ brew unlink openssl@3
Unlinking /opt/homebrew/Cellar/openssl@3/3.0.6... 0 symlinks removed.

$ brew link openssl@3
Warning: openssl@3 is keg-only and must be linked with `--force`.

If you need to have this software first in your PATH instead consider running:
  echo 'export PATH="/opt/homebrew/opt/openssl@3/bin:$PATH"' >> ~/.zshrc

$ brew link openssl@3 --force
Linking /opt/homebrew/Cellar/openssl@3/3.0.6... 5515 symlinks created.

If you need to have this software first in your PATH instead consider running:
  echo 'export PATH="/opt/homebrew/opt/openssl@3/bin:$PATH"' >> ~/.zshrc

$ brew cleanup
Warning: Skipping openssl@3: most recent version 3.0.5 not installed

```
