---
title: 【Docker】Dockerfileでヒアドキュメントを使用する方法
tags:
  - Docker
  - dockerfile
  - 初学者
private: false
updated_at: '2022-09-03T16:10:57+09:00'
id: d5a1ededc134cb001ca3
organization_url_name: null
slide: false
ignorePublish: false
---
## Dockerfileでヒアドキュメントを使用する方法
`Dockerfile`に以下のように記述することでヒアドキュメントを使用することができます。
ただし、Buildkitを使用している必要があります。

```Dockerfile:Dockerfile
# syntax=docker/dockerfile:1
ARG RUBY_IMAGE_TAG
FROM ruby:${RUBY_IMAGE_TAG}

ARG PROJECT_NAME
ARG RUBYGEMS_VERSION
ARG USER_NAME=ruby
ENV TZ=Asia/Tokyo

RUN adduser ${USER_NAME}

COPY --chown=${USER_NAME} Gemfile Gemfile.lock /${PROJECT_NAME}/

WORKDIR /${PROJECT_NAME}
RUN <<-EOF
  gem update --system ${RUBYGEMS_VERSION}
  bundle install
  chown -R ${USER_NAME} ${GEM_HOME}
EOF

COPY --chmod=755 /.docker/api/entrypoint.sh /usr/bin/
ENTRYPOINT ["entrypoint.sh"]

USER ${USER_NAME}
RUN mkdir -p /${PROJECT_NAME}/tmp/sockets/

EXPOSE 3000

CMD ["bundle", "exec", "pumactl", "start"]

```

https://github.com/moby/buildkit/blob/master/frontend/dockerfile/docs/reference.md#here-documents

`Dockerfile`に`# syntax=docker/dockerfile:1`を記述するのを忘れないようご注意ください。
`# syntax=docker/dockerfile:1`の`1`はバージョンの指定です。

https://hub.docker.com/r/docker/dockerfile

ヒアドキュメントの使用方法は以下をご参照ください。

https://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#tag_18_07_04
