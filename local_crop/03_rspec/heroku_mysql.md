# MySQLでHerokuデプロイする

HerokuではDBの初期設定は`Postgresql`になっているので変更処理を行う必要がある。

# デプロイまでの流れ

### 1. Herokuへログイン

```
$ heroku login
heroku: Press any key to open up the browser to login or q to exit:   #エンター押す
Opening browser to https://cli-auth.heroku.com/auth/cli/browser/3c35ddf6-f0a6-4911-9bd8-e9472b963bb8
Logging in... done
Logged in as [メールアドレス]
```

### 2. Heroku上でアプリ作成

アプリ名はユニークであることが必須である。  
また、アンダーバー`_`は使えないのでハイフン`-`を使う。  

```
$ cd [アプリ名]
$ heroku apps:create [アプリ名]
Creating ⬢ [アプリ名]... done
https://[アプリ名].herokuapp.com/ | https://git.heroku.com/[アプリ名].git

# [アプリ名]にアンダーバー等を含めると以下のようにエラーが生じます。
Creating ⬢ [アプリ名]... !
 ▸    Name must start with a letter, end with a letter or digit and can only contain lowercase letters, digits, and dashes.

# [アプリ名]がユニークでないとエラーが生じます。
Creating ⬢ [アプリ名]... !
 ▸    Name [アプリ名] is already taken
```

### 3. リモートリポジトリの確認

```
$ git remote -v
heroku  https://git.heroku.com/[アプリ名].git (fetch)
heroku  https://git.heroku.com/[アプリ名].git (push)
origin  https://github.com/[GitHubオーナー名]/[アプリ名].git (fetch)
origin  https://github.com/[GitHubオーナー名]/[アプリ名].git (push)
```

### 4. MySQLを追加

clearDBというクラウド上でMySQLを使うための無料サービスプランが有る。  
使用するには、予めクレジットカード登録が必要である。  
参考: [【Rails6, heroku】MySQLにしてmigrateしたけど有料化が必要だった件 - qiita](https://qiita.com/pharma_tech3/items/505b36e9bd3fc45afe65#heroku%E3%81%A7mysql%E3%82%92%E4%BD%BF%E3%81%88%E3%82%8B%E3%82%88%E3%81%86%E3%81%AB%E3%81%99%E3%82%8B)

```
$ heroku addons:create cleardb:ignite
Creating cleardb:ignite on ⬢ [アプリ名]... free
Created cleardb-objective-20233 as CLEARDB_DATABASE_URL
Use heroku addons:docs cleardb to view documentation
```

### 5. HerokuのアプリにDB情報の環境変数を設定

以下のコマンドで、環境変数に入る値を取得する。

```
$ heroku config
=== <アプリの名前> Config Vars
CLEARDB_DATABASE_URL: mysql://<ユーザー名>:<パスワード>@<ホスト名>/<データベース名>?reconnect=true
```
Herokuアプリの環境変数に、上記で取得した値をそれぞれ設定する。
```
$ heroku config:add DB_NAME='<データベース名>'

$ heroku config:add DB_USERNAME='<ユーザー名>'

$ heroku config:add DB_PASSWORD='<パスワード>'

$ heroku config:add DB_HOSTNAME='<ホスト名>'

$ heroku config:add DB_PORT='3306'

# gemで「mysql2」を使用しているので、mysql://ではなく「mysql2://」とする。
$ heroku config:add DATABASE_URL='mysql2://<ユーザー名>:<パスワード>@<ホスト名>/<データベース名>?reconnect=true'
```
設定した値を確認する。
```
$ heroku config

=== <アプリの名前> Config Vars
CLEARDB_DATABASE_URL: mysql://<ユーザー名>:<パスワード>@<ホスト名>/<データベース名>?reconnect=true
DATABASE_URL:         mysql2://<ユーザー名>:<パスワード>@<ホスト名>/<データベース名>?reconnect=true
DB_HOSTNAME:          <ホスト名>
DB_NAME:              <データベース名>
DB_PASSWORD:          <パスワード>
DB_PORT:              3306
DB_USERNAME:          <ユーザー名>
```

### 6. デプロイ

```
# master以外のブランチをpushする場合は以下を実行
$ git push heroku <ブランチ名>:master

$ heroku rake db:migrate

$ heroku open
```

# 参考

[HerokuでのアプリのデプロイでMySQLを使用してみた。 - qiita](https://qiita.com/Takao_/items/aeb3570b42a6aeb5461f)

[【Rails6, heroku】MySQLにしてmigrateしたけど有料化が必要だった件 - qiita](https://qiita.com/pharma_tech3/items/505b36e9bd3fc45afe65#heroku%E3%81%A7mysql%E3%82%92%E4%BD%BF%E3%81%88%E3%82%8B%E3%82%88%E3%81%86%E3%81%AB%E3%81%99%E3%82%8B)

[Herokuへのデプロイ方法](http://judo-engineer.blog.jp/archives/6853624.html)