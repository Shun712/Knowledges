# ドメイン取得方法

### 1. お名前ドットコム側の設定

1. お名前.comにアクセスし、ドメインNaviにログインする。

2. ログインすると上のメニューバーにDNSを押す。

3. ドメインのDNS関連機能設定にチェックを入れる。

4. 中央に表示される内部ドメイン一覧から今回使用したいドメイン名にチェックを入れる。

5. DNSレコード設定を利用するという項目があるんで、「設定する」ボタンを押す。

[![Image from Gyazo](https://i.gyazo.com/953657b27e864b39ce6ba524ebc0a31e.png)](https://gyazo.com/953657b27e864b39ce6ba524ebc0a31e)

6. TypeをCNAMEにし、VALUEに先ほどコピーしたDNS Targeを入力する。

[![Image from Gyazo](https://i.gyazo.com/d586010f2ef52397a6725b9460f150a5.png)](https://gyazo.com/d586010f2ef52397a6725b9460f150a5)

7. 設定を完了してから、20分くらいでドメインが反映される。

### 2. Herokuにドメインの登録

### 3. SSLの設定

# 参考

[Herokuで独自ドメインを使う方法【ついでにSSLにも対応】](https://freesworder.net/heroku-own-domain/)

[お名前.comを使い、独自ドメイン取得し、herokuデプロイする - qiita](https://qiita.com/tksh8/items/ab3748bcb01316461abe)

[お名前.comで購入したドメインをHerokuに設定する - qiita](https://qiita.com/ozin/items/62bc7ef1dd3c827177fb)

[Herokuアプリに独自ドメインを設定＆SSL化する](https://medium.com/@kjmczk/heroku-cdomain-ssl-1b4cae424e61#fb18)

[Herokuに独自ドメインを設定しSSL化する方法を画像で分かりやすく](https://blog.cloud-acct.com/posts/heroku-domain-settings/)