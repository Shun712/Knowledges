# database.ymlとは?

データベースに関する設定を行うファイルである。MySQL関連の設定をここで行う -ユーザIDやパスワードなどもここで設定する。

# ファイルの詳細

```
development:
  adapter: mysql2
  encoding: utf8
  database: sample_mysql_development
  pool: 5
  username: root
  password:
  host: localhost

test:
  adapter: mysql2
  encoding: utf8
  database: sample_mysql_test
  pool: 5
  username: root
  password:
  host: localhost

production:
  adapter: mysql2
  encoding: utf8
  database: sample_mysql_production
  pool: 5
  username: root
  password:
  host: localhost
```

```
adapter:   使用するデータベース種類
encoding:  文字コード
reconnect: 再接続するかどうか
database:  データベース名
pool:      コネクションプーリングで使用するコネクションの上限
username:  ユーザー名
password:  パスワード
host:      MySQLが動作しているホスト名
```

- MySQL接続用のアカウント作成

```
$ mysql -u root
:
:
mysql> create user 'ユーザー名'@'localhost' identified by 'パスワード';
```
`$ mysql -u root`でMySQLに接続をしアカウント名、パスワード、ホスト名を設定する。

```
mysql> select User,Host from mysql.user;
:
:
mysql> grant all on *.* to '[ユーザー名]'@'localhost';
```
`select User,Host from mysql.user;`で作成されているかを確認し、`grant all on *.* to '[ユーザー名]'@'localhost';`をしアカウントに権限を付与する。

- database.ymlの書き換え

```
development:
  adapter: mysql2
  encoding: utf8
  reconnect: false
  database: [アプリ名]_development
  pool: 5
  username:設定したユーザー名
  password:設定したパスワード
  host: localhost

test:
  adapter: mysql2
  encoding: utf8
  reconnect: false
  database: [アプリ名]_test
  pool: 5
  username:設定したユーザー名
  password:設定したパスワード
  host: localhost

production:
  adapter: mysql2
  encoding: utf8
  reconnect: false
  database: [アプリ名]_production
  pool: 5
  username:設定したユーザー名
  password:設定したパスワード
  host: localhost
```
これでMySQLにデータベース作成等の操作ができようになる。

# 参考

[【Rails】【DB】database.yml - qiita](https://qiita.com/ryouya3948/items/ba3012ba88d9ea8fd43d)

[mysql5.7 でユーザ追加の方法が変わったのでメモ（ユーザーに権限を与える）- qiita](https://qiita.com/waterada/items/b06a32a2b3afd4aac901)