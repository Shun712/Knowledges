# Form Objectとは?
Ruby on Railsのデザインパターン「設計手法」の1つである。  
もともと、modelにバリテーションなど様々な処理が書かれているものを、form層に切り出すことで多くのmodelで同一の処理を使えるなど、拡張性の高いコードを実現させることができる。

# Form Objectのメリット
1. DBを使わないフォームでも、ActiveRecordを利用した場合と同じ作法を利用できるので可読性が増す
2. 他の箇所に分散されがちなロジックをform object内に集めることができ、凝縮性を高められる

Form Objectを使う場面というのは、
**複数のモデルに跨がる場合、もしくはDBに保存する必要がないのでモデルがない場合**(インスタクローンはこのパターン)のときであり、ActiveModelの特性をincludeすることでモデルのようなものを作ることができる。

Form Objectを使わない場合、
例えば、コントローラにロジックを記述してファットコントローラーとなったり、独自の作法でフォームを作成するため、ビューとコントローラを両方読まないとどのように動くのか理解できないため、可読性が下がる。  

# Form Objectを使わない例

以下は、フィードバックをDBに保存せずに、サビース管理者へメール送信をするようにするコードである。
```ruby
class FeedbacksController < ApplicationController
  def new
  end

  def create
    if params[:title].present? && params[:body].present?
      AdminMailer.feedback(params[:title], params[:body]).deliver_later
      redirect_to home_path, notice: 'フィードバックを送信しました'
    else
      @error_messages = []
      @error_messages << 'タイトルを入力してください' if params[:title].blank?
      @error_messages << '本文を入力してください' if params[:body].blank?
      render :new
    end
  end
end
```

```ruby
<%= form_with url: feedbacks_path, local: true do %>
  <% @error_messages && @error_messages.each do |message| %>
    <%= message %>
  <% end %>
  <%= label_tag :title %>
  <%= text_field_tag :title, params[:title] %>
  <%= label_tag :body %>
  <%= text_area_tag :body, params[:body] %>
  <%= submit_tag %>
<% end %>
```
コントローラーに記述が増えてしまい、ビューとコントローラーを両方見なければすぐに理解できない。

# Form Objectを使う例

```ruby
class Feedback
  # ActiveModel::Modelを使えるようにする
  include ActiveModel::Model
  attr_accessor :title, :body

  validates :title, :body, presence: true

  def save
    return false if invalid?
    AdminMailer.feedback(title, body).deliver_later
    true
  end
end

class FeedbacksController < ApplicationController
  def new
    @feedback = Feedback.new
  end

  def create
    @feedback = Feedback.new(feedback_params)
    if @feedback.save
      redirect_to home_path, notice: 'フィードバックを送信しました'
    else
      render :new
    end
  end

  private

  def feedback_params
    params.require(:feedback).permit(:title, :body)
  end
end
```
```ruby
<%= form_with model: @feedback, local: true do |f| %>
  <% if @feedback.errors.any? %>
    <% @feedback.errors.full_messages.each do |message| %>
      <%= message %>
    <% end %>
  <% end %>
  <%= f.label :title %>
  <%= f.text_field :title %>
  <%= f.label :body %>
  <%= f.text_area :body %>
  <%= f.submit %>
<% end %>
```
Feedbackクラスを除けば、ActiveRecordを利用した例と同じコードになる。

# 参考

[form objectを使ってみよう](https://tech.medpeer.co.jp/entry/2017/05/09/070758)

[Form Object という選択肢を検討してみる](https://www.fundely.co.jp/blog/tech/2020/04/08/180009/)

[accepts_nested_attributes_forを使わず、複数の子レコードを保存する](https://moneyforward.com/engineers_blog/2018/12/15/formobject/)
