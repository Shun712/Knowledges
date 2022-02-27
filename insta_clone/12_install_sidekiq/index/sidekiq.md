# Sidekiqとは?

Rails アプリで**非同期処理を行うためのライブラリ**である。  
つまり、非同期処理を行うためのサーバーのようなもので`ActiveJob`(rails)とredisの橋渡し的役割をしている。
導入することで複数のジョブを同時に実行でき、メモリを節約できる。

# 全体像

[![Image from Gyazo](https://i.gyazo.com/e647c1eb318d5a132048b7a7df3c7e6b.png)](https://gyazo.com/e647c1eb318d5a132048b7a7df3c7e6b)

# Sidekiqの実装手順

#### 1. インストール

前提条件として、`Redis`が必要になるのでインストールする。  
`Redis`はキューの受け皿となり、キューが保存されるので(メール送信処理などの)ジョブが永続される。  
また、`Sidekiq`には、ジョブの処理状況をGUIで確認できるインターフェースが用意されている。  
そのインターフェースは`sinatra`で動いているため、`sinatra`のインストールが必要となる。

`brew install redis`  
`gem 'sidekiq'`  
`gem 'sinatra'`

#### 2. ジョブを実装(メール送信処理)

(app/mailers/user_mailer.rb)
```ruby
class UserMailer < ApplicationMailer
  def comment_post
    @user_from = params[:user_from]
    @user_to = params[:user_to]
    @comment = params[:comment]
    mail(to: @user_to.email, subject: "#{@user_from.username}があなたの投稿にコメントしました")
  end
end 
```

(app/controllers/comments_controller.rb)
```ruby
class CommentsController < ApplicationController
  def create
    @comment = current_user.comments.build(comment_params)
    UserMailer.with(user_from: current_user, user_to: @comment.post.user, comment: @comment).comment_post.deliver_later if @comment.save
  end
end 
```

#### 3. Sidekiqにキューを定義

(config/sidekiq.yml)
```ruby
:concurrency: 25
:queues:
  - default
  - mailers
```

`$ bundle exec sidekiq -q default -q mailers`でも起動できるが、  
設定ファイルを用意しておくことで、起動時に読み込んでくれる。  
`$ bundle exec sidekiq -C config/sidekiq.yml`

#### 4. ActiveJobのアダプターとしてSidekiqを指定

バックグラウンド(ジョブ管理)でキューを処理するサーバーとして`Sidekiq`を指定

(config/application.rb)
```ruby
module InstaRails
  class Application > Rails::Application
    config.active_job.queue_adapter = :sidekiq
  end
end
```

#### 5. ブラウザから監視できるようツールを実装

(config/routes.rb)
```ruby
require 'sidekiq/web'
mount Sidekiq::Web => '/sidekiq'
```
[![Image from Gyazo](https://i.gyazo.com/628d7b574b55cf98c4691e96fed41491.png)](https://gyazo.com/628d7b574b55cf98c4691e96fed41491)

# 参考

[sidekiq - github](https://github.com/mperham/sidekiq/wiki/Active-Job)

[[Ruby on Rails] Sidekiq で非同期処理を実装する](https://dev.classmethod.jp/articles/ruby-on-rails-sidekiq/)

[Railsで非同期処理を行える「Sidekiq」 - qiita](https://qiita.com/yumiyon/items/6835d90e621e73268021)

