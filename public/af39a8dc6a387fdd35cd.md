---
title: 【Dokcer】全ファイルをボリュームで管理する【Remote-Containers】
tags:
  - Docker
  - 初学者
  - Next.js
  - Remote-Containers
private: false
updated_at: '2022-05-30T03:03:20+09:00'
id: af39a8dc6a387fdd35cd
organization_url_name: null
slide: false
ignorePublish: false
---
## 全ファイルをボリュームで管理する
### Docker
```Dockerfile:/Dockerfile
FROM node:16.15.0

ENV TZ=Asia/Tokyo
ARG USERNAME=node

RUN corepack enable npm
USER ${USERNAME}
WORKDIR /myapp-frontend

EXPOSE 3000

```

```/docker-compose.yml
version: '3.9'
services:
  frontend:
    build: .
    volumes:
      - .:/myapp-frontend
    environment:
      NODE_ENV: development
    ports:
      - 3000:3000
      - 9229:9229
    volumes:
      - sources:/myapp-frontend
    command: /bin/sh -c "while sleep 1000; do :; done"
volumes:
  sources:
```

### Remote-Containers

```.devcontainer/devcontainer.json
{
  "name": "myapp-frontend",
  "dockerComposeFile": ["../docker-compose.yml"],
  "service": "frontend",
  "workspaceFolder": "/myapp-frontend",
  "customizations": {
    "vscode": {
      "extensions": [
        "EditorConfig.EditorConfig",
        "dbaeumer.vscode-eslint",
        "esbenp.prettier-vscode",
        "VisualStudioExptTeam.vscodeintellicode",
        "arcanis.vscode-zipfs",
        "bradlc.vscode-tailwindcss"
      ]
    }
  }
}
```

