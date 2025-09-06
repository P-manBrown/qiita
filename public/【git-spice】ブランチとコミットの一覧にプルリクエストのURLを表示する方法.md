---
title: 【git-spice】ブランチとコミットの一覧にプルリクエストのURLを表示する方法
tags:
  - git-spice
private: false
updated_at: '2025-09-06T23:57:18+09:00'
id: 628000f6d5a4b4bfe0ef
organization_url_name: null
slide: false
ignorePublish: false
---
## 設定方法

`spice.log.crFormat`設定によって、ブランチとコミットの一覧にプルリクエストの情報を表示できます。

```bash
# プルリクエストのURLを表示する設定
git config --local spice.log.crFormat "url"

# プルリクエストのIDを表示する設定（デフォルト）
git config --global spice.log.crFormat "id"
```

### gs log short（短縮表示）の設定

```bash
git config --global spice.logShort.crFormat "url"
```

### gs log long（詳細表示）の設定

```bash
git config --global spice.logLong.crFormat "url"
```

## 例

### 設定前の表示（IDでの表示）

```bash
$ gs log long
```

```
  ┏━■ feature/user-profile-settings (#456) ◀
  ┃   b3c2d1e feat: add user profile settings page (2 hours ago)
┏━┻□ feature/authentication-system (#455)
┃    f7e6a9b feat: implement authentication system (1 day ago)
main
```

### 設定後の表示（URLでの表示）

```bash
$ git --global config spice.log.crFormat "url"
$ gs log long
```

```
  ┏━■ feature/user-profile-settings (https://github.com/example-org/sample-app/pull/456) ◀
  ┃   b3c2d1e feat: add user profile settings page (2 hours ago)
┏━┻□ feature/authentication-system (https://github.com/example-org/sample-app/pull/455)
┃    f7e6a9b feat: implement authentication system (1 day ago)
main
```

## 参考

https://abhinav.github.io/git-spice/cli/config/#spiceloglongcrformat
