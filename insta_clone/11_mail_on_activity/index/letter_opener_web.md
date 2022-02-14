# letter_opener_webとは?

開発環境で送信したメールをブラウザで確認することができるgemである。  
ローカル環境で確認できるので、メール送受信機能を実装した際には必須のgemである。  

> Gives letter_opener an interface for browsing sent emails.
> [letter_opener_web - github](https://github.com/fgrehm/letter_opener_web)

# 実装手順

#### 1. gemの導入

```ruby
group :development do
  gem 'letter_opener_web', '~> 1.0'
end
```

#### 2. ルーティングの設定

```ruby
Rails.application.routes.draw do
  if Rails.env.development?
    mount LetterOpenerWeb::Engine, at: '/letter_opener'
  end
end 
```

#### 3. config/environments/development.rbの編集

```ruby
Rails.application.configure do
  # 省略
  config.action_mailer.default_url_options = { host: 'localhost:3000' }
  config.action_mailer.delivery_method = :letter_opener_web
end
```

`config.action_mailer.default_url_options = { host: 'localhost:3000' }`では、  
アプリケーションのホスト情報をメイラー内で使いたい場合、`:host` パラメータを明示的に指定する。  

> *_pathヘルパーは、動作の性質上メール内では一切利用できない点にご注意ください。メールでURLが必要な場合は*_urlヘルパーを使ってください。
> [2.7 Action MailerのビューでURLを生成する - Railsガイド](https://railsguides.jp/action_mailer_basics.html#action-mailer%E3%81%AE%E3%83%93%E3%83%A5%E3%83%BC%E3%81%A7url%E3%82%92%E7%94%9F%E6%88%90%E3%81%99%E3%82%8B)

(app/views/user_mailer/comment_post.html.slim)
```ruby
h2 = "#{@user_to.username}さん"
p = "#{@user_from.username}さんがあなたの投稿にコメントしました。"
= link_to "確認する", post_url(@comment.post, { anchor: "comment-#{@comment.id}" })
```

これだけの設定でブラウザでメールを確認することができる。

# 参考

[Action Mailer の基礎 - Railsガイド](https://railsguides.jp/action_mailer_basics.html)

[letter_opener_web - github](https://github.com/fgrehm/letter_opener_web)

[gem letter_opener を試してみる - qiita](https://qiita.com/tanutanu/items/c6193c4c2c352ac152ec)

[【Rails】letter_opener_webを用いて開発環境で送信したメールを確認する方法](https://techtechmedia.com/letter_opener_web/)
