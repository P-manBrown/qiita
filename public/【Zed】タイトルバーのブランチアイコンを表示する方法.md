---
title: 【Zed】タイトルバーのブランチアイコンを表示する方法
tags:
  - ZedEditor
private: false
updated_at: '2025-11-21T23:56:11+09:00'
id: bc91d9ce49dd6049ae6e
organization_url_name: null
slide: false
ignorePublish: false
---

## 設定方法

`settings.json`に`title_bar`の`show_branch_icon`プロパティを以下のとおり追記します。

```json
{
  "title_bar": {
    "show_branch_icon": true
  }
}
```

![screen-shot-741.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/7fa5639c-fc86-4ea0-b6ec-dcd2b20658b9.png)

## その他のタイトルバー設定

タイトルバーでは、ブランチアイコン以外にも様々な要素の表示を制御できます。
```jsonc
{
  "title_bar": {
    "show_branch_icon": false,    // ブランチアイコンの表示/非表示
    "show_branch_name": true,      // ブランチ名の表示/非表示
    "show_project_items": true,    // プロジェクト名の表示/非表示
    "show_onboarding_banner": true,// オンボーディングバナーの表示/非表示
    "show_user_picture": true,     // ユーザーアバターの表示/非表示
    "show_sign_in": true,          // サインインボタンの表示/非表示
    "show_menus": false            // メニューの表示/非表示
  }
}
```

## 参考

https://zed.dev/docs/visual-customization#titlebar
