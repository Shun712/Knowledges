# Herokuで環境変数を設定

ローカルリポジトリの`.env`ファイル内で設定している環境変数をHerokuに設定しなければ、Herokuは環境変数を呼び出せない。

# 設定方法

### 1. Herokuコマンドで設定

`$ heroku config:set 環境変数名=値`

`$ heroku config:set 環境変数名1=値1 環境変数名2=値2`

**このとき、`=`の間に空白文字を入れない**

### 2. サイトから設定

herokuサイトからsettingタブをクリックして環境変数を設定する。

[![Image from Gyazo](https://i.gyazo.com/17635078884038f73abccde6fef6a095.png)](https://gyazo.com/17635078884038f73abccde6fef6a095)

# 参考

[【Heroku】Herokuで環境変数を設定する方法 - qiita](https://qiita.com/mzmz__02/items/64db94b8fc67ee0a9068)