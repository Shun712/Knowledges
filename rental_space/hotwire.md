# Hotwireとは？

大量のJavaScriptを使わず、モダンなWebアプリケーションを作るためのアプローチ

- JSONではなく、HTMLベース
- サーバーサイドでHTMLを生成し、`WebSocket`でWebブラウザへ送信
- 構成する主な要素
  - Turbo
  - Stimulus

# Hotwireを使うメリット

- Rails6以前の環境
  - 最新バージョンjs(ES6)を使いたい
    - →主要なブラウザが対応していないので、ブラウザで動作するES5にトランスパイルする必要がある
- そのために必要なパッケージとその役割
  - node.js
    - ES6のjsをサーバー側で解釈するために必要
    - ES6のjsをES5にトランスパイルするため、`node.js`に`babel`をインストール
    - `node.js`に`webpack`をインストール
  - webpacker
    - webpackを使うためRubyGem
    - webpackはES6で使うモジュールをまとめてトランスパイルするために必要
  - yarn
    - node.jsで使うパッケージやES6のモジュールをインストール

[![Image from Gyazo](https://i.gyazo.com/3d4c74129f7b0caec871a3a840afa864.jpg)](https://gyazo.com/3d4c74129f7b0caec871a3a840afa864)

Rails6では、ES6のjsを使うため上記のようなパッケージを使う必要があった。

- 外部環境の変化
  - 主要なブラウザがES6に対応
    - ES6のトランスパイルが不要に
  - HTTP/2の普及
    - 小さなファイルを非同期で送信可能
    - Webpackでのファイル結合が不要に
  - Importmap
    - JSモジュールの論理的参照

# どんなことができるのか

Rails7のデフォルト設定では`node.js`、`yarn`をインストールする必要がない。`yarn`で使っていたパッケージは`importmaps`で対応する。

# 参考

[Rails 7のHotwireを簡単に理解する](https://techblog.gmo-ap.jp/2022/07/05/rails-7-hotwire/)

[Hotwireかんたん入門](https://note.com/everyleaf/n/n842f5020d43b)