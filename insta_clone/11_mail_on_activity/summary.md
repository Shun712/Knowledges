# 11 メール通知

# やったこと
- メール通知機能を実装してください。
- タイミングと文言は以下の通りとします。
    - フォローされたとき
    - 自分の投稿にいいねがあったとき
    - 自分の投稿にコメントがあったとき

# Action Mailerとは?
**Ruby on Rails**に備わっているメール送信機能のこと。  
**Action Mailer** を使うと、**Ruby on Rails**からメール送信をしてくれる。  
アプリケーションのメーラークラスやビューからメールを送信することができる便利な機能である。

> [Action Mailerとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/11_mail_on_activity/index/action_mailer.md)

# letter_opener_webとは?
開発環境で送信した**メールをブラウザで確認する**ことができるgemである。  
ローカル環境で確認できるので、メール送受信機能を実装した際には必須のgemである。

> [letter_opener_webとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/11_mail_on_activity/index/letter_opener_web.md)

# gem configとは？

Ruby on Railsで便利に定数を管理することができるgemである。

# 詰まった(ている)こと

メール送信でメール本文に記載されている
`= link_to "確認する", post_url(@comment.post, { anchor: "comment-#{@comment.id}" })`
の`post_url`でエラーが発生しております。

### エラーログ
```
[ActiveJob] [ActionMailer::Parameterized::DeliveryJob] [8bc26035-32bd-449f-a690-b5442bd6125e] Error performing ActionMailer::Parameterized::DeliveryJob (Job ID: 8bc26035-32bd-449f-a690-b5442bd6125e) from Async(mailers) in 17.14ms: ActionView::Template::Error (Missing host to link to! Please provide the :host parameter, set default_url_options[:host], or set :only_path to true):
```

`ActionView::Template::Error (Missing host to link to! Please provide the :host parameter, set default_url_options[:host]`とあり、ホスト情報がメイラー内でうまく設定されていないと思いましたが、以下のように設定されています。

(config/environments/development.rb)
```ruby
Rails.application.configure do
  # 省略
  config.action_mailer.default_url_options = Settings.default_url_options.to_h
  config.action_mailer.delivery_method = :letter_opener_web
end
```

(config/development.yml)
```ruby
default_url_options:
  host: 'localhost:3000'
```

### 試したこと
- configのバージョンを 3.1.1 から 2.1.1 に下げて見ましたが、エラーが発生しておりました。

- RubyMineからconfigのgemがrbenvのバージョン2.6.4に対応していないというヒント?を提示されバージョンを2.7.5に上げましたが変わりませんでした。

#### 参考にしたページ

[RailsでMissing host to link to!が出たときに。model内でURL組み立てる場合の設定 - qiita](https://qiita.com/daik/items/41a9bc8dec5ccec37f40)

[【Rails】'ArgumentError (Missing host to link to! Please provide the :host parameter, set default_url_options[:host], or set :only_path to true):'が出たときの対処法 - qiita](https://qiita.com/hirochan/items/7c4f24bf05d9de8a196b)

ご教授お願いします。
