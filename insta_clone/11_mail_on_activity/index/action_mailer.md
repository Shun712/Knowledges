# Action Mailerとは?

**Ruby on Rails**に備わっているメール送信機能のこと。  
**Action Mailer** を使うと、**Ruby on Rails**からメール送信をしてくれる。  
アプリケーションのメーラークラスやビューからメールを送信することができる便利な機能である。

今回は、通知機能としてメールを送信する。

# 導入手順

#### 1. メイラーの生成

railsコマンド(rails generate)で生成する。`UserMailer`は任意クラス名。

```ruby
$ rails generate mailer UserMailer
      create  app/mailers/user_mailer.rb
      invoke  slim
      create  app/views/user_mailer
```

#### 2. サーバーの設定

`config/environments/development.rb`にメール送信設定を記述する。
今回は、`config.action_mailer`というパラメータに`letter_opener_web` オプションを使う。
```ruby
Rails.application.configure do
  config.action_mailer.delivery_method = :letter_opener_web
end
```

#### 3. メーラーを編集

メーラーはRailsのコントローラーと似ており、「アクション」と呼ばれるメソッドがある。  
また、そのアクションからビューが呼び出される。

今回は、投稿にコメントされたら、投稿者にメールが届くようにする。

`application_mailer`には全メーラー共通の設定をする。  
`user_mailer.rb`にはメーラー個別の設定をする。

###### application_mailerを編集する

```ruby
class ApplicationMailer < ActionMailer::Base
  default from: 'insta@example.com'
  layout 'mailer'
end
```
ここでは、メール送信者のアドレスを`insta@example.com`にする。
layoutメソッドでは、各ページ共通ファイルをlayoutsディレクトリの`mailer`が呼び出される。

###### user_mailer.rbを編集する

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
個別の設定には`mail`メソッドを使用する。
`comment_post`メソッドを呼び出すときに、渡されるユーザーの情報からメールアドレスをメール送信先とする。  
`mail`メソッドが呼び出されると、メール本文が記載されているビューが読み込まれる。  
インスタンス変数で値をビューに渡したいので用意する。


#### 4. メール本文を作成する

顧客によっては、HTMLファイルのメールを受け取れない/受け取りたくない人もいるので場合によっては、テキストメールも作成しておく必要がある。

(app/views/user_mailer/comment_post.html.slim)
```ruby
h2 = "#{@user_to.username}さん"
p = "#{@user_from.username}さんがあなたの投稿にコメントしました。"
= link_to "確認する", post_url(@comment.post, { anchor: "comment-#{@comment.id}" })
```

#### 5. 処理を走らせるアクションにメール送信処理させる

```ruby
class CommentsController < ApplicationController
  def create
    @comment = current_user.comments.build(comment_params)
    UserMailer.with(user_from: current_user, user_to: @comment.post.user, comment: @comment).comment_post.deliver_later if @comment.save
  end
end 
```
メーラー(`application_mailer.rb` / `user_mailer.rb`)は**各コントローラーのアクションからの呼び出し**によって起動する。  
`with`に渡されるキーの値は、メイラーアクションでは単なる`params`になる。つまり、`with(user_from: current_user, user_to: @comment.post.user, comment: @comment)`とすることで メイラーアクションで`params[:user_from]`や`params[:user_to]`や`params[:comment]`を使えるようになる。 ちょうどコントローラのparamsと同じ要領である。

# 参考

[Action Mailer の基礎 - Railsガイド](https://railsguides.jp/action_mailer_basics.html)

[Action Mailer でメール送信機能をつくる](https://qiita.com/annaaida/items/81d8a3f1b7ae3b52dc2b)