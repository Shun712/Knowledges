# redisとは？

NoSQLの中でも、KVS(キーバリューストア)。キーとバリューの組み合わせを保存するソフトウェア。
Redisのデータはすべてメモリ内に保存されるため、高速なデータの読み書きが可能である。
また、セッションデータの場合は、Redisへ変更することでセッションハイジャックなどのセキュリティリスクを軽減できる。

# 仕組み

[![Image from Gyazo](https://i.gyazo.com/5cd7f4ed6a97708035eb48f9ecdf8cb6.png)](https://gyazo.com/5cd7f4ed6a97708035eb48f9ecdf8cb6)

# 導入方法

1. Redis のインストール
`$ brew install redis`

2. Redis サーバーの起動
`$ redis-server`

これでローカル環境で Redis を使えるようになる。

# Railsのセッション管理をRedisにしてみる

1. redis-railsをGemfileに追記
`gem 'redis-rails`

2. bundle install
`$ bin/bundle install`

3. `config/initializers/session_store.rb`を新規に作成しセッション管理をRedisにするための設定を記述
```
# config/initializers/session_store.rb
アプリケーション名::Application.config.session_store :redis_store, {
  servers: [
    {
      host: "localhost",  # Redisのサーバー名
      port: 6379,         # Redisのサーバーのポート
      db: 0,              # データベースの番号(0 ~ 15)の任意
      namespace: "session"  # 名前空間。"session:セッションID"の形式
    },
  ],
  expire_after: 90.minutes # 保存期間
}
```

# 参考

[Redisとは？RailsにRedisを導入](https://qiita.com/hirotakasasaki/items/9819a4e6e1f33f99213c)

[【Rails入門】Redisでセッションを高速化しよう！キャッシュも解説](https://www.sejuku.net/blog/58218)

[Redisの紹介](https://www.sraoss.co.jp/tech-blog/redis/redis-introduction/)
