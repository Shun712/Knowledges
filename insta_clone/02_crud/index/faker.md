# fakerとは?

ダミーデータを作成する際に、ある項目のデータを自動で出力してくれるgemである。

# 実装手順

#### 1. Fakerのインストール

```
group :development, :test do
  gem 'faker'
end
```

`bundle install`

#### 2. ファイルにデータを作成
ファイルの構造
```
db # 関係あるファイルだけ表示
├── seeds
│   ├── users.rb
│   └── posts.rb
└── seeds.rb
```

(db/seeds.rb)
```
require './db/seeds/users'
require './db/seeds/posts'
```

(db/seeds/users.rb)
```
puts 'Start inserting seed "users" ...'
10.times do
  user = User.create(
    email: Faker::Internet.unique.email,
    username: Faker::Internet.unique.user_name,
    password: 'password',
    password_confirmation: 'password'
    )
  puts "\"#{user.username}\" has created!"
end
```
`unique`オプションをつけると、デフォルトでユニークなデータが生成されるようになる。
また、最後にputsを利用して、出力されるキャラクターの名前を書き出している。

(db/seeds/posts.rb)
```
puts 'Start inserting seed "posts" ...'
User.limit(10).each do |user|
  post = user.posts.create(body: Faker::Hacker.say_something_smart, remote_images_urls: %w[https://picsum.photos/350/350/?random https://picsum.photos/350/350/?random])
  puts "post#{post.id} has created!"
end
```
`Lorem Picsum`というgemを使用。画像を返してくれる便利サービスである。
`remote_images_urls:` というカラムは、「https://~~~.jpg」のような外部から取ってきた画像を設定する。
「remote_カラム名_url」とすれば使える。
> [Github: carrierwave](https://github.com/carrierwaveuploader/carrierwave#uploading-files-from-a-remote-location)

# 参考

[Github: carrierwave](https://github.com/carrierwaveuploader/carrierwave#uploading-files-from-a-remote-location)

[gem Fakerでリアルなダミーデータを作るよ - qiita](https://qiita.com/tanutanu/items/4006bd868affa535adb0)

[【Rails】seed.rbとFakerを使ってダミーデータ作ってみた - Zenn](https://zenn.dev/yukihaga/articles/e0cf573f3c545e)