# ngrokとは?

ngrokは「エングロック」と発音し、トンネリングを用いて
ローカルPCのWebサーバーを外部公開できるツールである。

# ngrokの使用目的

コンテンツを公開するのに、いちいちクラウドをアップしてという煩わしい手順を踏まずすむ。  
また、メタタグが反映されているか確認できたりと様々な面で便利である。

# 手順

#### 1. ngrokにユーザー登録

[公式サイト](https://dashboard.ngrok.com/get-started/setup) から
登録できる。

#### 2. ngrokをインストール

`$ brew install nginx`

#### 3. ローカルサーバーを起動

`$ rails server`

#### 4. ngrokによるWebサイトの公開

`$ ngrok http 3000`

ローカルで起動しているページのポート番号を入れて起動し以下のようになれば成功。

```ruby
Session Status                online
Session Expires               7 hours, 59 minutes
Version                       2.3.35
Region                        United States (us)
Web Interface                 http://127.0.0.1:4040
Forwarding                    http://1fd2ec17.ngrok.io -> http://localhost:3000
Forwarding                    https://1fd2ec17.ngrok.io -> http://localhost:3000

Connections                   ttl     opn     rt1     rt5     p50     p90
0       0       0.00    0.00    0.00    0.00
```

#### 5. アクセス

httpの場合  
`http://1fd2ec17.ngrok.io`  
httpsの場合  
`https://1fd2ec17.ngrok.io`

#### 6. セキュリティの設定

Chromeのセキュリティ関係でアクセスできなければ、セキュリティの強度を一時的に下げる。

# 参考

[ngrokインストール方法と簡単な使い方](https://www.mgo-tec.com/blog-entry-ngrok-install.html)

[ngrokが便利すぎる - qiita](https://qiita.com/mininobu/items/b45dbc70faedf30f484e)

[ngrokの利用方法 - qiita](https://qiita.com/Marusoccer/items/7033c1bb9c85bf6789bd)

