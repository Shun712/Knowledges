# Rails deviseによるメールによるユーザー認証

メール認証によるユーザー登録は当たり前の実装になるので実装手順を残しておく。

# 実装手順

### 1. SMTPサーバーの設定

メールを実際に送信するには、SMTPサーバーを設定する。  
今回は、gmailを用いてメールの送信を行う。  
githubに間違って公開しないように、`dotenv-rails`や`config`を用いる。

```ruby
# config/environments/development.rb
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
config.action_mailer.raise_delivery_errors = true
config.action_mailer.delivery_method = :smtp
config.action_mailer.smtp_settings = {
  address: 'smtp.gmail.com',
  port: 587,
  user_name: ENV['GMAIL_ADDRESS'],
  password: ENV['GMAIL_PASSWORD'],
  authentication: :plain,
  enable_starttls_auto: true
}
```

### 2. メール認証機能を追加

[この記事](https://qiita.com/kskumgk63/items/aa581b6b3f8c66fa82e2#%E3%83%A1%E3%83%BC%E3%83%AB%E8%AA%8D%E8%A8%BC%E6%A9%9F%E8%83%BD%E3%82%92%E8%BF%BD%E5%8A%A0-1)
を参照する。

### 3. confirmable機能の有効化

```ruby
# app/models/user.rb
class User < ApplicationRecord
  # Include default devise modules. Others available are:
  # :confirmable, :lockable, :timeoutable, :trackable and :omniauthable
  devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :validatable, :confirmable #←ココに追加だけ
  #以下略#
end
```

# 逆にメールを送りたくない場合

deviseには、`skip_confirmation! `メソッドが用意されており、メール認証をスキップすることができる。  
ポイントは**Userデータが登録される前**に、このメソッドを使うことである。
```ruby

def self.create(auth)
  user = User.new(
    username: auth['info']['name'],
    email: auth['info']['email'] || Faker::Internet.email,
    password: Devise.friendly_token[0, 20]
  )
  
  # 以下の１行を追記
  user.skip_confirmation!
  
  user.save!
  user.social_profiles.create!(
    provider: auth['provider'],
    uid: auth['uid'])
  user
end
```

# 参考

[Rails deviseによるユーザー認証 メールによる認証、emailとusernameのどちらでもログイン可能にするまで - qiita](https://qiita.com/shizuma/items/c8c2e71af8c1dcf3d1c2)

[deviseを使ったログイン機能を実装する！メール認証機能付き - qiita](https://qiita.com/kskumgk63/items/aa581b6b3f8c66fa82e2)

[【Rails】deviseでURL認証付きのメールを送信してみる - qiita](https://qiita.com/ozackiee/items/21fcad4a1564136b9510)

[deviseのTwitterログイン時はメール認証とメール送信をスキップする - qiita](https://qiita.com/tegnike/items/a655c5ee7f71fb5bef08)