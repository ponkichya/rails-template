# Rails プロジェクト新規作成の仕方

## Rails プロジェクトを作成

`$ docker-compose run web rails new . --force --no-deps --database=mysql`

## コンテナをビルド

`$ docker-compose build`

## データベースファイルの修正

上記実行後、config/database.yml ファイルを下記の通りに修正

```
default: &default
  adapter: mysql2
  encoding: utf8mb4
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password:
  host: localhost

development:
  <<: *default
  database: myapp_development
  host: db
  username: root
  password: password

test:
  <<: *default
  database: myapp_test
  host: db
  username: root
  password: password
```

## データベースを作成

`$ docker-compose run web rails db:create`

## Webpacker をインストール

Rails 6 系から Webpacker が必要
web サーバのコンテナに webpacker をインストール
`$ docker-compose run web rails webpacker:install `

## docker-compose でコンテナを起動

`$ docker-compose up -d`

## アクセスして起動を確認

ブラウザから **_localhost:3000_** にアクセスし、Rails の初期画面が表示されることを確認して完了
