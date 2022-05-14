# お問い合わせ機能を実装

### 1. DBを作成

```ruby
class CreateFeedbacks < ActiveRecord::Migration[6.1]
  def change
    create_table :feedbacks do |t|
      t.string :name, null: false
      t.string :email, null: false
      t.text :body, null: false

      t.timestamps
    end
  end
end
```

### 2. コントローラの実装

```ruby
class FeedbacksController < ApplicationController
  skip_before_action :authenticate_user!

  def new
    @feedback = Feedback.new
  end

  def create
    @feedback = Feedback.new(feedback_params)
    if @feedback.save
      UserMailer.with(user_from: @feedback.name,
                      feedback: @feedback).feedback.deliver_later
      redirect_to new_feedback_path, success: 'お問い合わせ内容を送信しました。'
    else
      flash[:danger] = '送信に失敗しました。'
      redirect_to new_feedback_path
    end
  end

  private

  def feedback_params
    params.require(:feedback).permit(:name, :email, :body)
  end
end
```

### 3. ビューの実装

```ruby
# app/views/feedbacks/new.html.slim

/! Contact form
.container.py-4.py-lg-5.my-4
  .row
    .col-md-8.offset-md-2
      .card.border-0.shadow
        .card-body
          h2.h4.text-center.mb-3 お問い合わせフォーム
          p.fs-sm.text-muted ご意見、ご不明な点がございましたら下記のフォームからご連絡ください。
          = form_with model: @feedback, class: 'needs-validation mb-3', local: true do |f|
            .row.g-3
              .col-sm-6
                = f.label :name
                = f.text_field :name, autofocus: true, autocomplete: "username", placeholder: "山田 太郎", class: "form-control rounded-start", required: ""
              .col-sm-6
                = f.label :email
                = f.email_field :email, autofocus: true, autocomplete: "email", placeholder: "taro_yamada@email.com", class: "form-control rounded-start", required: ""
              .col-12
                = f.label :body
                = f.text_area :body, autofocus: true, autocomplete: "body", placeholder: "お問い合わせ内容を入力してください。", class: "form-control rounded-start", required: "", rows: 6
            .text-end.pt-4
              = f.submit '送信', class: 'btn btn-primary mt-4'
```

### 4. ルーティング

```ruby
Rails.application.routes.draw do
  resources :feedbacks, only: %i[new create]
end
```

### 5. モデルの実装

ユーザーが間違ってメールアドレスに大文字を含めてアカウント登録してしまった際に、`before_save`コールバックを用いて小文字に変換できる。

```ruby
class Feedback < ApplicationRecord
  validates :name, presence: true, length: { maximum: 50 }
  VALID_EMAIL_REGEX = /\A[\w+\-.]+@[a-z\d\-.]+\.[a-z]+\z/i.freeze
  validates :email, presence: true, length: { maximum: 255 },
            format: { with: VALID_EMAIL_REGEX }
  before_save :downcase_email
  validates :body, presence: true, length: { maximum: 1000 }
end
```

# 参考

[コールバック - Railsガイド](https://railsguides.jp/active_record_callbacks.html#%E5%88%A9%E7%94%A8%E5%8F%AF%E8%83%BD%E3%81%AA%E3%82%B3%E3%83%BC%E3%83%AB%E3%83%90%E3%83%83%E3%82%AF)

[Ruby on Rails でレビュー機能を実装する - qiita](https://qiita.com/Jumpei_Sogawa/items/0a1bda821a88d45bcf12)

[【Ruby on Rails】お問合せフォームの作成 - qiita](https://qiita.com/japwork/items/145645e281b81d9bf92c)

[わたしがRailsチュートリアルで学んだこと【6章】- qiita](https://qiita.com/ShinKano/items/daeed93201701b35d7b0)