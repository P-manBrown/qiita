---
title: 【Thunder Client】devcontainer内でThunder Clientを使用する
tags:
  - 初学者
  - devcontainer
  - ThunderClient
private: false
updated_at: '2023-02-14T21:20:02+09:00'
id: b25ca3b47fa4e5db6f5c
organization_url_name: null
slide: false
ignorePublish: false
---
## Dev Containersの設定

devcontainer内にThunder　Clientがインストールされるように`.devcontainer/devcontainer.json`の`customizations.vscode.extensions`に`rangav.vscode-thunder-client`を追加します。

```json:devcontainer.json
{

...

  "customizations": {
    "vscode": {
      "extensions": [
        ...
        "rangav.vscode-thunder-client"
      ]
    }
  }
}
```

## データの永続化

Thunder Clientのデータを永続化するために`.devcontainer/compose.devcontainer.yml`を作成して既存の`compose.yml`をオーバーライドします。

Thunder Clientのデータは`~/.vscode-server/data/User/globalStorage/rangav.vscode-thunder-client`に保存されます。
上記の情報は`~/.th-client/thunder-cache.json`に記述されています。

```json:thunder-cache.json
{"globalPath":"/home/user/.vscode-server/data/User/globalStorage/rangav.vscode-thunder-client"}
```

`~/.vscode-server/data/User/globalStorage/rangav.vscode-thunder-client`にボリュームマウントを設定するため`compose.devcontainer.yml`を次のように記述します。

```yaml:compose.devcontainer.yml
services:
  api:
    volumes:
      - th-client-storage:/home/user/.vscode-server/data/User/globalStorage/rangav.vscode-thunder-client
    command: bash -c "while sleep 1000; do :; done"
volumes:
  th-client-storage:

```

devcontainer起動時に`compose.devcontainer.yml`が読み込まれるように`.devcontainer/devcontainer.json`の`dockerComposeFile`に`./compose.devcontainer.yml`を追加します。

```json:devcontainer.json
{
  ...

  "dockerComposeFile": ["../compose.yml", "./compose.devcontainer.yml"],

  ...

}

```

devcontainerをrootで実行している場合には上記で問題ないと思いますがDockerfile内で一般ユーザーに変更している場合にはdevcontainer起動時に次のようなエラーとなります。

```
mkdir: cannot create directory ‘/home/user/.vscode-server/bin’: Permission denied
```

`~/.vscode-server/data/User/globalStorage/rangav.vscode-thunder-client`にボリュームマウントを設定したためコンテナ起動時にrootで`.vscode-server`ディレクトリが作成されることが原因です。

`.vscode-server`の所有者を変更するため次の内容で`.devcontainer/devcontainer-entrypoint.sh`を作成します。

```devcontainer-entrypoint.sh
#!/usr/bin/env bash

set -eu

user="$(whoami)"
sudo chown -R "${user}" "/home/${user}/.vscode-server"

exec "$@"

```

コンテナ内で`sudo`を使用できるようにするため`devcontainer.json`の`features`に次の記述を追加します。

```json:devcontainer.json
{
  "features": {
    "ghcr.io/devcontainers/features/common-utils:2": {},
  }
}
```

コンテナ起動時に上記のファイルを実行するため`compose.devcontainer.yml`を編集します。


```compose.devcontainer.yml
services:
  api:
    volumes:
      - th-client-storage:/home/user/.vscode-server/data/User/globalStorage/rangav.vscode-thunder-client
    entrypoint:
      - bash
      - ./.devcontainer/devcontainer-entrypoint.sh
    command: bash -c "while sleep 1000; do :; done"
volumes:
  th-client-storage:

```

これでdevcontainerが起動できるようになります。

## `localhost`の代わりに`host.docker.internal`を使用する

devcontainer内でThunder
