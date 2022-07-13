# Herokuコマンド

### ログイン・ログアウト

```
$ heroku login

Enter your Heroku credentials.
Email: メールアドレス
Password (typing will be hidden): 
Authentication successful.
```

```
$ heroku logout

Local credentials cleared.
```

### ログの確認

```
$ heroku logs
```

```
リアルタイム
$ heroku logs -t

or

$ heroku logs --tail
```

### ステータス確認

```
$ heroku ps
```

## コマンド実行

```
$ heroku run "コマンド"
```

### Rails consoleを実行

```
$ heroku run rails c
```

## 環境変数

### 確認

```
$ heroku config
```

### 追加

```
$ heroku config:set PASSWORD=hogepiyopassword
```

# 参考

[Heroku コマンド・設定 メモメモ - qiita](https://qiita.com/pugiemonn/items/0e69b7a29a384b356e65)