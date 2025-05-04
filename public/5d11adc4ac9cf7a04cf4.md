---
title: 【Docker】Rails + Puma + Nginx + MySQL + React
tags:
  - Rails
  - MySQL
  - nginx
  - Docker
  - React
private: false
updated_at: '2022-04-01T03:54:31+09:00'
id: 5d11adc4ac9cf7a04cf4
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに
　本記事は、プログラミング初学者、学習を進めていて疑問に思った点について調べた結果を備忘録も兼ねてまとめたものです。
　そのため、記事の内容に誤りが含まれている可能性があります。ご容赦ください。
　間違いを見つけた方は、お手数ですが、ご指摘いただけますと幸いです。

## Rails + Puma + Nginx + MySQL + React
```docker-compose.yml 
version: '${COMPOSE_VER}'
services:
  db:
    platform: linux/x86_64
    build: ./docker/db
    command: --default-authentication-plugin=mysql_native_password && bash -c "chmod +x /docker-entrypoint-initdb.d/00_grant.sh"
    healthcheck:
      test: mysqladmin ping -h db -u$${MYSQL_USER} -p$${MYSQL_PASSWORD}
      interval: 1s
    restart: on-failure
    volumes:
      - mysql_data:/var/lib/mysql
      - type: bind
        source: ${MY_CNF_PATH}
        target: /etc/mysql/conf.d/my.cnf
      - type: bind
        source: ${INITDB_PATH}
        target: /docker-entrypoint-initdb.d
    env_file:
      - ${DB_ENV_FILE_PATH}
    ports:
      - "${DB_PORT}:3306"
  api:
    build:
      context: .
      dockerfile: ./docker/api/Dockerfile
    command: bash -c "mkdir -p ./tmp/sockets && bundle exec puma -C config/puma.rb"
    restart: on-failure
    volumes:
      - .:/myapp
      - public-data:/myapp/public
      - tmp-data:/myapp/tmp
    environment:
      RAILS_ENV: ${APP_ENV}
    ports:
      - "${API_PORT}:3000"
    depends_on:
      db:
        condition: service_healthy
  web:
    build: ./docker/web
    volumes:
      - public-data:/myapp/public
      - tmp-data:/myapp/tmp
    ports:
      - 80:80
    depends_on:
      - api
volumes:
  mysql_data:
  public-data:
    driver_opts:
      type: none
      device: ${PWD}/public
      o: bind
  tmp-data:
     driver_opts:
      type: none
      device: ${PWD}/tmp
      o: bind
```

```.env
COMPOSE_VER = 3.9

# db-variables.env
DB_ROOT_PASSWORD = myappdbrootpassword
DEV_DATABASE_NAME = myapp_development
TEST_DATABASE_NAME = myapp_test
DB_USER_NAME = user
DB_USER_PASSWORD = userpassword

# docker-compose.yml_db
DB_IMAGE_TAG = 8.0.28
MY_CNF_PATH = ./docker/db/my.cnf
INITDB_PATH = ./docker/db/docker-entrypoint-initdb.d
DB_ENV_FILE_PATH = ./docker/db/db-variables.env
DB_PORT = 3306

# docker-compose.yml_api
APP_ENV = development
API_PORT = 3001

```

### Rails

```Dockerfile:Dockerfile
FROM ruby:3.1.1
ENV APP_NAME=myapp
ENV USER_NAME=myuser
ENV TZ=Asia/Tokyo

WORKDIR /${APP_NAME}

COPY Gemfile /${APP_NAME}/Gemfile
COPY Gemfile.lock  /${APP_NAME}/Gemfile.lock
RUN bundle install

COPY /docker/api/entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]

RUN adduser ${USER_NAME} && \
    chown -R ${USER_NAME} /${APP_NAME} && \
    chown -R ${USER_NAME} ${GEM_HOME}
USER ${USER_NAME}

EXPOSE 3000

CMD ["rails", "server", "-b", "0.0.0.0"]
```
```entrypoint.sh
#!/bin/bash

set -e

rm -f /myapp/tmp/pids/server.pid

exec "$@"
```
```Gemfile:Gemfile
source "https://rubygems.org"
gem "rails", "~> 7.0.2", ">= 7.0.2.3"
```

### MySQL
```Dockerfile:Dockerfile
FROM mysql:8.0.28

ENV USER_NAME=myuser
ENV TZ='Asia/Tokyo'

RUN adduser ${USER_NAME}

USER ${USER_NAME}

```
```00_grant.sh
#!/bin/bash

mysql=( mysql -uroot -p"${MYSQL_ROOT_PASSWORD}" )

"${mysql[@]}" <<-EOSQL
    CREATE DATABASE IF NOT EXISTS ${MYSQL_TEST_DATABASE};
    GRANT ALL ON ${MYSQL_TEST_DATABASE}.* TO '${MYSQL_USER}'@'%' ;
EOSQL
```
```my.cnf
[mysqld]
character-set-server=utf8mb4
collation-server=utf8mb4_general_ci

[client]
default-character-set=utf8mb4
```
``` database.yml
default: &default
  adapter: mysql2
  encoding: utf8mb4
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: <%= ENV["DB_USER_NAME"] %>
  password: <%= ENV["DB_USER_PASSWORD"] %>
  host: db

development:
  <<: *default
  database: <%= ENV["DEV_DATABASE_NAME"] %>

test:
  <<: *default
  database: <%= ENV["TEST_DATABASE_NAME"] %>

production:
  <<: *default
  database: myapp_production
  username: myapp
  password: <%= ENV["MYAPP_DATABASE_PASSWORD"] %>

```

### Nginx

```Dockerfile:Dockerfile
FROM nginx:1.21.6

RUN rm -f /etc/nginx/conf.d/*

COPY nginx.conf /etc/nginx/conf.d/myapp.conf

ENV USER_NAME=myuser
RUN adduser ${USER_NAME} && \
    chown -R ${USER_NAME} /var/cache/nginx/ && \
    chown -R ${USER_NAME} /var/run/
USER ${USER_NAME}

CMD /usr/sbin/nginx -g 'daemon off;' -c /etc/nginx/nginx.conf
```

```nginx.conf

upstream myapp {
  server unix:///myapp/tmp/sockets/puma.sock;
}

server {
  listen 80;

  server_name localhost;
  access_log /var/log/nginx/access.log;
  error_log  /var/log/nginx/error.log;

  root /myapp/public;

  client_max_body_size 100m;
  error_page 404             /404.html;
  error_page 505 502 503 504 /500.html;
  try_files  $uri/index.html $uri @myapp;
  keepalive_timeout 5;

  location @myapp {
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Host $http_host;
    proxy_pass http://myapp;
  }
}
```
```puma.rb
threads_count = ENV.fetch("RAILS_MAX_THREADS") { 5 }
threads threads_count, threads_count
environment ENV.fetch("RAILS_ENV") { "development" }
plugin :tmp_restart

app_root = File.expand_path("../..", __FILE__)
bind "unix://#{app_root}/tmp/sockets/puma.sock"

stdout_redirect "#{app_root}/log/puma.stdout.log", "#{app_root}/log/puma.stderr.log", true
```

### React
```docker-compose.yml
version: '3.9'
services:
  front:
    build: .
    volumes:
      - .:/myapp/front
    environment:
      NODE_ENV: development
    command: sh -c "npm start"
    ports:
      - 3000:3000
    networks:
      - nginxrailspumamysql_default
networks:
  nginxrailspumamysql_default:
    external: true

```
```Dockerfile:Dockerfile
FROM node:16.14.2

ENV APP_NAME=myapp
ENV USER_NAME=myuser
ENV TZ=Asia/Tokyo

WORKDIR /${APP_NAME}/front

RUN adduser ${USER_NAME} && \
  chown -R ${USER_NAME} /${APP_NAME}
USER ${USER_NAME}

EXPOSE 3000
CMD ["npm", "start"]
```
