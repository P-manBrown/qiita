---
title: 【VSCode】PlantUMLの導入方法
tags:
  - PlantUML
  - VSCode
  - 初学者
private: false
updated_at: '2023-02-05T23:51:08+09:00'
id: 46dfdd974b2aecde099a
organization_url_name: null
slide: false
ignorePublish: false
---
## ローカルの場合
次のコマンドを実行します。  

```terminal
brew install --cask temurin
brew install graphviz
```

VSCodeの拡張機能をインストールします。  

https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml

以下のいずれかの拡張子のファイルを作成します。  

- `*.wsd`
- `*.pu`
- `*.puml`
- `*.plantuml`
- `*.iuml`

作成したファイルの内容を編集します。  

```sample.pu
@startuml Sample
hide circle
skinparam linetype ortho

entity user as "user" {
  *user_id [PK]
  --
  created_at [作成日]
  updated_at [更新日]
}

entity user_profile as "user_profile" {
  *user_profile_id [PK]
  --
  *user_id [FK]
  name [名前]
  email [メールアドレス]
  password [パスワード]
  created_at [作成日]
  updated_at [更新日]
}

entity post as "post" {
  *post_id [PK]
  --
  *user_id[FK]
  title [タイトル]
  body [内容]
  created_at [作成日]
  updated_at [更新日]
}

user ||-d-|| user_profile
user ||-r--o{ post

@enduml

```

`alt`+`D`またはコマンドパレットから`PlantUML: カーソル位置のダイアグラムをプレビュー`を実行します。  
すると以下のようにプレビューが表示されます。  

![image221230_224108.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/fa6c6589-ece5-fb81-ffe3-fba8cc921270.png)

## PlantUML Serverの場合

次のコマンドを実行します。  

```terminal
docker run -d -p 8080:8080 plantuml/plantuml-server:jetty
```

拡張機能をインストールして設定を以下のとおり変更します。  

```settings.json
{
  "plantuml.server": "http://localhost:8080",
  "plantuml.render": "PlantUMLServer"
}
```

以降はローカルの場合と同様です。  

- 参考

https://github.com/plantuml/plantuml-server
