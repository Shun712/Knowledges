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

# 参考

[【図解】Dockerの全体像を理解する -前編- - qiita](https://qiita.com/etaroid/items/b1024c7d200a75b992fc)