---
title: 【Docker】Dockerfileで親ディレクトリを参照する方法
tags:
  - Docker
  - dockerfile
  - docker-compose
  - 初学者
private: false
updated_at: '2022-03-24T04:36:09+09:00'
id: fcb2dbd71bfa6be49cf8
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに
　本記事は、プログラミング初学者、学習を進めていて疑問に思った点について調べた結果を備忘録も兼ねてまとめたものです。
　そのため、記事の内容に誤りが含まれている可能性があります。ご容赦ください。
　間違いを見つけた方は、お手数ですが、ご指摘いただけますと幸いです。

## Dokerfileで親ディレクトリを参照する方法
Dokerfileで親ディレクトリを参照するにはDocker-composeのbuildの箇所でcontextとdockerfileを指定します。

```docker-compose.yml
version: '3.9'
services:
  api:
    build:
      context: .
      dockerfile: ./docker/api/Dockerfile
    command: bash -c "rm -f tmp/pids/server.pid && bundle exec rails s -p 3000 -b '0.0.0.0'"
    # restart: on-failure
    volumes:
      - .:/myapp
    environment:
      RAILS_ENV: ${APP_ENV}
    ports:
      - "${API_PORT}:3000"
    depends_on:
      db:
        condition: service_healthy

```

Dockerfileには親ディレクトリから見たパスを記述します。

```Dockerfile:Dockerfile
FROM ruby:3.1.1

WORKDIR /myapp

COPY Gemfile /myapp/Gemfile
COPY Gemfile.lock  /myapp/Gemfile.lock
RUN bundle install

COPY docker/api/entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]

EXPOSE 3000

ENV TZ=Asia/Tokyo

CMD ["rails", "server", "-b", "0.0.0.0"]
```
