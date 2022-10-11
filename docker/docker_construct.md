# Rails環境構築

1. ディレクトリを作成する

`$ mkdir Documents/Rails_Docker`

2. 作成したディレクトリに移動

`$ cd Documents/Rails_Docker`

3. GitHubからクローン

`$ git clone https://github.com/xxx/xxx.git`

4. クローンしたディレクトリに移動する。

`$ cd Rails_Todo`

5. Dockerfileを作成

`$ touch Dockerfile`

# Dockerfile

```Dockerfile
# ベースとなるイメージの指定（rubyのバージョン3.0.3を指定）
FROM ruby:3.0.3
 
# ビルド(build)時に実行するコマンドの指定
# インストール可能なパッケージの一覧の更新
RUN apt-get update -qq \
# パッケージのインストール（nodejs、postgresql-client、npmを指定）
&& apt-get install -y nodejs postgresql-client npm \
&& rm -rf /var/lib/apt/lists/* \
&& npm install --global yarn
 
# 作業ディレクトリの指定
WORKDIR /myapp
COPY Gemfile /myapp/Gemfile
COPY Gemfile.lock /myapp/Gemfile.lock
RUN bundle install
# Add a script to be executed every time the container starts.
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000
# Configure the main process to run when running the image
CMD ["rails", "server", "-b", "0.0.0.0"]
```

6. docker-compose.ymlを作成

# docker-compose.yml

```yaml
version: "3"
services:
  db:
    # コンテナ名の指定
    container_name: rails_todo_db
    # イメージの指定
    image: postgres:14.2-alpine
    # データの永続化（ホスト側のtmp/dbディレクトリにマウントする）
    volumes:
      - ./tmp/db:/var/lib/postgresql/data
    # 環境変数の指定（初期設定値）
    environment:
      POSTGRES_PASSWORD: password
  web:
    # コンテナ名の指定
    container_name: rails_todo_web
    # Dockerfile のあるディレクトリのパスを指定（imageかbuildを必ず指定する必要がある）
    build: .
    # デフォルトのコマンド指定（Rails特有の問題解消とRails立ち上げを指定している）
    command: bash -c "rm -f tmp/pids/server.pid && bundle exec rails s -p 3000 -b '0.0.0.0'"
    # データの永続化（ホスト側のカレントディレクトリにマウントする）
    volumes:
      - .:/myapp
    # ポートの指定（外部からのアクセス時のポート：Dockerコンテナからアクセス時のポート）
    ports:
      - "3000:3000"
    # 依存関係の指定（dbが起動した後に、webが起動するようになる）
    depends_on:
      - db
```

# entrypoint.sh

Rails固有の問題を修正するためのファイルです。`server.pid`というファイルがネックになるため、毎回削除する。

7. entrypoint.shを作成

```sh
set -e
 
# Remove a potentially pre-existing server.pid for Rails.
rm -f /myapp/tmp/pids/server.pid
 
# Then exec the container's main process (what's set as CMD in the Dockerfile).
exec "$@"
```

8. サービスを構築する

`$ docker-compose build`

9. 立ち上げ

`$ docker-compose up -d`

10. コンテナに入る

`$ docker container exec -it rails_todo_web bash`

11. マイグレーション

`$ docker container exec -it rails_todo_web bash`

12. アクセスして動作確認

`http://localhost:3000`

# 参考

[DockerでRails環境を構築してみた](https://rightcode.co.jp/blog/information-technology/docker-rails-environment-setup-syain)