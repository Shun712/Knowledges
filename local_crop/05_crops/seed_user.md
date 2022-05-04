# deviseを利用したusersテーブルでseed.rbからユーザーを作成する

deviseを利用していると、`confirmable`モジュールがあるため確認済みが必要となる。

# 発生するエラー

```ruby
A confirmation email was sent to your account at 'example@example.com'.
You must follow the instructions in the email before your account can be activated"
```

# 解決方法

確認処理を無くしたい場合には、新規Userを作成する時に`confirmed_at`に値が入っている必要がある。

```ruby
user = User.create(
    email: Faker::Internet.unique.email,
    username: Faker::Internet.unique.user_name,
    password: 'password',
    password_confirmation: 'password',
    confirmed_at: Time.now
```

# 参考

[Deviseのconfirmableをオンにした時の挙動の変化の仕組みを理解する - qiita](https://qiita.com/Coolucky/items/30884d93db7afca2b2c7)

[devise で作成した users テーブルに seeds.rb からユーザを作成する](https://yshystsj.com/2019/05/26/post-174/)