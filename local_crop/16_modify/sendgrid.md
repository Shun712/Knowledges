# sendgridでメール送信を設定

sendgirdはメールのインフラサービスである。

# 実装手順

### 1. sendgridにてアカウント登録

sendgridが使えるようにアカウント登録し、メール認証する。

### 2. APIキーを発行する

メール認証が終わったら、APIキーを作成するので、左メニューバーから 「Settingsタブ」内にある「API Keys」を選択する。

右上の「Create API Key」を押すと下の画面になるので、「API Key Names」にアプリの名称を入力し、「Full Access」 を選択し、「Create & View」をクリック。

[![Image from Gyazo](https://i.gyazo.com/ac6fc33bf2fc9c99753d6d0bf3431de5.png)](https://gyazo.com/ac6fc33bf2fc9c99753d6d0bf3431de5)

### 3. Herokuの環境変数にSendGridのAPIKeyを追加

**Rails6アプリの設定にAPIキーを直書きするのは危険なので必ず環境変数を使う。**

`$ heroku config:set SENDGRID_API_KEY=作成したAPIキー`

### 4. smtpを使う

- 開発環境

```ruby
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
  config.action_mailer.raise_delivery_errors = false
  config.action_mailer.delivery_method = :smtp
  config.action_mailer.smtp_settings = {
    address: 'smtp.sendgrid.net',
    port: 587,
    domain: 'localhost',
    user_name: 'apikey',
    password: ENV['SENDGRID_API_KEY'],
    authentication: :plain,
    enable_starttls_auto: true
  }
```

- 本番環境

```ruby
config.active_record.dump_schema_after_migration = false
  config.action_mailer.default_url_options = { host: "#{ENV['HOST']}/" }
  config.action_mailer.raise_delivery_errors = true
  config.action_mailer.delivery_method = :smtp
  config.action_mailer.smtp_settings = {
    enable_starttls_auto: true,
    address: 'smtp.sendgrid.net',
    port: 587,
    domain: ENV['DOMAIN'],
    authentication: :plain,
    user_name: 'apikey',
    password: ENV['SENDGRID_PASSWORD']
  }
```

### 5. 送信元のメールアドレスを変更する

送信元のメールアドレスを変更したいときは、config/initialisers/devise.rbの下記の部分を編集すれば送信元のメアドにも反映される。

```ruby
# config/initialisers/devise.rb

config.mailer_sender = 'example@example.com'
```

# 参考

[sendgridを使ってメールを送信 Rails - qiita](https://qiita.com/ibarakishiminn/items/e8bf4246242921c2cdd4)

[Ruby on Rails ~ deviseでアプリにユーザー認証、サインアップ、ログイン機能をつける(開発環境&本番環境)（コードメモ）- qiita](https://qiita.com/wtb114/items/176c19bd9caff0893d7c)

[【Rails】SendGridでメール送信(2021年3月) - qiita](https://qiita.com/d0ne1s/items/4bc26378c1eb7f9a19cc)

[Rails+Heroku+SendGrid環境でのメール送信機能を作成する](https://twin-t.com/railsherokusendgrid%E7%92%B0%E5%A2%83%E3%81%A7%E3%81%AE%E3%83%A1%E3%83%BC%E3%83%AB%E9%80%81%E4%BF%A1%E6%A9%9F%E8%83%BD%E3%82%92%E4%BD%9C%E6%88%90%E3%81%99%E3%82%8B/)

[Rails6 アプリからメールを送信する デプロイ環境編](https://qiita.com/miriwo/items/46a58bd92f74f0dc74d8)

[Rails Action MailerでSendGrid Web APIを使用する - qiita](https://qiita.com/yoshixj/items/34692d760b889299f9b9)

[Heroku+SendGrid+Rails6（devise）の本番環境でメール送信する方法](https://asalworld.com/rails-heroku-sendgrid/)

[SendGridを使ってSMTPでメールを送信する方法](https://blog.kozakana.net/2018/05/rails-sendgrid-smtp/)

[Rails Heroku で運用しているサイトで SendGrid を2段階認証にし API KEY を利用して SMTP 方式で Mail を送信する -qiita](https://qiita.com/1024xx4/items/04ee9b9028615a5d0693)

[【Rails7】開発環境、本番環境でメール送信できるようにする（SendGrid, Gmail）](https://kobacchi.com/rails-mail-server-sendgrid-gmail/)