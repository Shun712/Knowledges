# form_with

`form_with`は渡されたものによって、行うHTTPメソッドとアクションをそれぞれ判断してくれる。

# form_with url: url_path

```ruby
<%= form_with url: users_path do |form| # urlを渡している %>
  <%= form.text_field :email %>
  <%= form.submit %>
<% end %>
```
`users_path`に対してPOSTを行い、このコードであれば
params[:email]
のような形で`text_field`に入力された値を取得する。

# form_with model: @model

モデルに入っているものが**①新しく作られたものの場合、と②既存のものを呼び出した場合、で処理が変わってくる**

```ruby
<%= form_with model: @user do |form| # modelを渡している %>
  <%= form.text_field :email %>
  <%= form.submit %>
<% end %>
```

#### ①. 新しく作られたものが渡された場合  
モデル(@user)の中身が空であることから、**createメソッド**を呼び出す

#### ②. 既存のものが渡された場合
`new.html.erb`と`edit.html.erb`のフォーム部分は全くの一緒  
モデル(@user)の中身があることから**updateメソッド**を呼び出すことを判断

[![Image from Gyazo](https://i.gyazo.com/4a3bb257ace674fb6c70e5d01a038ce9.png)](https://gyazo.com/4a3bb257ace674fb6c70e5d01a038ce9)

#### modelオプションのさらなる特徴

modelを使うとinputタグのvalueを指定してくれる。
例えば、検索フォームに入力した値が検索後のページでも値が残っている。

> [ActionView::Helpers::FormHelper](https://api.rubyonrails.org/classes/ActionView/Helpers/FormHelper.html#method-i-form_with)

#  form_with model: [@modelA, @modelB]
```ruby
resources :tweets do
  resources :comments only: [:index, :create]
end
```
(app/controllers/comments_controller.rb)
```ruby
def index
  # モデルを2つ用意
  @tweet = Tweet.find(params[:id])
  @comment = Comment.new
end
```
(app/views/comments/index.html.erb)
```ruby
<%= form_with(model:[@tweet, @comment]) do |form| %>
  <%= form.text_field :content %>
  <%= form.submit %>
<% end %>
```
複数モデルを受け取ると、1つ目が中身あり、2つ目が中身なしということで、それぞれから`tweets/:id/messages`というパスを自動で判断し、さらに中身なしということで`comment_controller.rb`のcreateを呼び出す。

[![Image from Gyazo](https://i.gyazo.com/5b89d78d7d8bc71038b3ea41fbac27c2.png)](https://gyazo.com/5b89d78d7d8bc71038b3ea41fbac27c2)

# 参考

[【Rails】form_with/form_forについて【入門】 - qiita](https://qiita.com/snskOgata/items/44d32a06045e6a52d11c#23-form_with-model-modela-modelb)