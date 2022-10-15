# Dockerの全体像

### 仮想化

PCやサーバーといったマシンにインストールされているOS（ホストOS）の上に、別のマシンを仮想的に立ち上げること

### コンテナ型仮想化

[![Image from Gyazo](https://i.gyazo.com/f0a199143ad1ee7b41012e1505f7aabf.png)](https://gyazo.com/f0a199143ad1ee7b41012e1505f7aabf)

ホストOS上に動作している`Docker Engine`からコ**ンテナと呼ばれるミドルウェアの環境構築がされた実行環境を作成し、その中でアプリケーションを動作させる**。

### Dockerのメリット

- プログラム実行環境を管理するための仕組みとしてDockerがある。

- 環境ファイルを共有するための仕組みとしてDockerHubなどのサービスがある。

### 0. Docker Engine

Dockerを利用するための常駐プログラム

### 1. イメージ(image)

コンテナ起動に必要なファイルをまとめたもので「Imageはコンテナの元で、Imageからコンテナを起動する」

#### タグ(Tag)

Tagとは「imageのversion」のことである。

#### imageの構造

- イメージはレイヤー構造になっている。

- imageからコンテナを起動して、そのコンテナ内で何らかのミドルウェアをインストールした場合、それがコンテナレイヤに保存される。

- そのコンテナから再びimageを生成（commit）できる。

[![Image from Gyazo](https://i.gyazo.com/4d8c8e9cd751f6f62a8ea98e16d722f7.png)](https://gyazo.com/4d8c8e9cd751f6f62a8ea98e16d722f7)

#### Imageを用意する

ローカルに取得しているImage一覧を確認する。

`$ docker images`

imageを用意する方法

1. 他人が作ったimageを取得する(主にDocker Hubから)

`$ docker pull イメージ名     #Docker Hubなどからイメージを取得`

2. 自分で作る(他人のimageを改良する)

Dockerfile という名前のtextファイルを作り、その中にimage build(image作成)に関わる設定を記述して、Dockerfileからイメージを自作する。

```Dockerfile
FROM イメージ名:タグ名　　　　　　　#どのimageを元にimageを作成するか
RUN パッケージ等インストールコマンド     #ここに記述したコマンドを実行してミドルウェアをインストールし、imageのレイヤーを重ねる
CMD コマンド指定　　　　　　　　#コンテナが作成された後で実行するコマンドを指定する
```

`$ docker build -t ビルドしたイメージに付けるイメージ名 .`

一度buildしたimageを、Dockerfileの変更なしに再びbuildする際は、`build cache`が効いて、以前buildした情報を見に行くようになっているので、RUNにupdateコマンドなど記述していたとしても普通にbuildした直後は、そのコマンドは実行されないことになる。

cacheを無効にしてbuildする場合(何か変更した場合)  
`$ docker build —no-cache -t docker-whale`

### 2. コンテナ

imageを用意したら、そのイメージからコンテナ(アプリケーション実行環境)が起動する。

#### imageからコンテナ起動

```
docker pull :DockerHubからイメージを取得
docker create ：取得したイメージからコンテナを作成
docker start ：作成したコンテナを起動
```
を同時に実行するコマンドが`docker run`コマンドである。

#### コンテナの操作コマンド

##### コンテナ一覧を確認

現在実行中のコンテナを表示

`$ docker ps`

現在存在しているコンテナ一覧を表示

`$ docker ps -a`

##### コンテナの詳細確認

`$ docker inspect コンテナ名`

##### コンテナの作成

`$ docker create —name コンテナにつける名前 -it イメージ名 /bin/bash`

-i はコンテナの標準入力を取得して双方向接続するオプション  
-t はコンテナ内にTTYを割り当てるオプション  
**コンテナでシェルを実行して、フォアグラウンドで実行状態にしておきたい場合､ -itの組み合わせで使われる。これを付けないとシェルがすぐに終了してコンテナが停止する**


##### コンテナの起動

`$ docker start コンテナ名`

##### コンテナの削除

`docker rm コンテナ名`

##### 起動中のコンテナのシェルへ接続

起動時に `-it`フラグをつけている場合は、`control + p, control + q`で抜けるとコンテナは終了しない。

`$ docker exec -it 起動中のコンテナ名 /bin/bash`

##### コンテナからイメージを作成

`$ docker commit コンテナ名 image名：タグ名`

[![Image from Gyazo](https://i.gyazo.com/303f143900db74f158f17b8052a2eb50.png)](https://gyazo.com/303f143900db74f158f17b8052a2eb50)

### 4. Dockerにおけるデータ管理

起動したコンテナ内で扱う動的データは、

- コンテナが削除された時点で、そのコンテナ内のデータは消える

- コンテナ間でデータ共有はできない。

というデメリットが有る。

そのため、Dockerではホストマシン上にデータを管理し、それをコンテナにマウントする手法が取られる。

[![Image from Gyazo](https://i.gyazo.com/94a3ba859d99fbd47afb3a03f8de73b9.png)](https://gyazo.com/94a3ba859d99fbd47afb3a03f8de73b9)

### 5. Dockerネットワーク

例えば、Webアプリケーションサーバーの運用を行う場合、APIサーバコンテナとMySQLコンテナを立ち上げるとすると、APIサーバコンテナはMySQLコンテナと通信をする必要がある。

[![Image from Gyazo](https://i.gyazo.com/fd6b4bd7022b974225711ccfddca8f69.png)](https://gyazo.com/fd6b4bd7022b974225711ccfddca8f69)

### 6. Docker Compose

- `Docker Compose`は複数コンテナのDockerアプリケーションを事前定義して実行するためのツールである。

- Webサービスの実行環境をDockerで構築する場合、Webサーバー、DBサーバー、Cacheサーバーなど定義を一つの`docker-compose.yml`ファイルに記述しておくことで、必要なコンテナをまとめて起動・設定できる。

1. Dockerfileを用意する または Docker Hubなどに使用するイメージを用意する

2. docker-compose.ymlを定義する

3. ymlファイルがあるディレクトリで、`$ docker-compose up`を実行する

[![Image from Gyazo](https://i.gyazo.com/1455131cbac0a336ce80e57f122c5cac.png)](https://gyazo.com/1455131cbac0a336ce80e57f122c5cac)

#### docker-compose管理コマンド一覧

docker-composeで起動したコンテナの一覧を表示

`$ docker-compose ps`

docker-compose.ymlに記述した設定からコンテナ起動(再起動も)

`$ docker-compose up`

docker-composeで作成されたコンテナやネットワークを削除

`$ docker-compose down`

指定したサービスコンテナ内でコマンド実行

`$ docker-compose run [コンテナ名] [コマンド]`

一連のコンテナ停止

`$ docker-compose stop`

一連のコンテナ起動

`$ docker-compose start`

docker-composeによるアプリ実行環境構築例

#### docker-composeによるアプリ実行環境構築例

1. imageの用意

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

2. docker-compose.ymlの作成

```yaml
version: "3" # docker-composeのversion指定
services: # 起動するサービスコンテナを書いていく
  db: # dbサーバーコンテナを起動
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
  web: # webサーバーコンテナを起動
    # コンテナ名の指定
    container_name: rails_todo_web
    # Dockerfile のあるディレクトリのパスを指定（imageかbuildを必ず指定する必要がある）
    build: .
    # デフォルトのコマンド指定（Rails特有の問題解消とRails立ち上げを指定している）
    command: bash -c "rm -f tmp/pids/server.pid && bundle exec rails s -p 3000 -b '0.0.0.0'"
    # データの永続化（ホスト側のカレントディレクトリにバインドマウントする）
    volumes:
      - .:/myapp
    # ポートの指定（外部からのアクセス時のポート：Dockerコンテナからアクセス時のポート）
    ports:
      - "3000:3000"
    # 依存関係の指定（dbが起動した後に、webが起動するようになる）
    depends_on:
      - db
```

3. docker-composeの実行

`$ docker-compose up -d`

デタッチドモード(-d : バックグラウンド)で一連のコンテナを起動する。

[![Image from Gyazo](https://i.gyazo.com/b70af93ca51ff77650c4b542fae704e6.png)](https://gyazo.com/b70af93ca51ff77650c4b542fae704e6)

# 参考

[【図解】Dockerの全体像を理解する -前編- - qiita](https://qiita.com/etaroid/items/b1024c7d200a75b992fc)

[【図解】Dockerの全体像を理解する -中編- - qiita](https://qiita.com/etaroid/items/88ec3a0e2d80d7cdf87a)
