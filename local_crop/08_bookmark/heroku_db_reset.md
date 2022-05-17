# HerokuのMySQLデータベースをリセットする

RailsチュートリアルだとherokuのDBリセットコマンドは、

`$ heroku pg:reset DATABASE`

となっているので、MySQLのデータベースだとリセットされない。  
MySQLの場合、別のコマンドを実行する必要がある。

# 方法1: コマンドで対応

`$ heroku run rails db:migrate:reset RAILS_ENV=production DISABLE_DATABASE_ENVIRONMENT_CHECK=1`

アプリを指定する場合には、以下のコマンドを実行sる。

`$ heroku run --app アプリ名 rails db:migrate:reset RAILS_ENV=production DISABLE_DATABASE_ENVIRONMENT_CHECK=1`

# 方法2: MySQLにログインして

1. ユーザーなどを確認

`$ heroku config`

このコマンドを実行して、`ユーザー名，パスワード，ホスト，データベース`を取得する。

`DATABASE_URL: mysql2://ユーザー名:パスワード@ホスト/データベース?reconnect=true`

2. ログイン

取得した`ユーザー名，ホスト`を使用してログインする。

`$ mysql -h ホスト -u ユーザー名 -p`

3. 削除

MySQLのコマンドを参照。

# 参考

[Heroku本番環境のMySQLデータベースをリセットする方法 - qiita](https://qiita.com/take18k_tech/items/7afdde59d387fbde5f7e)