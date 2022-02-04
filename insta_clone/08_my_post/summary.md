# 08 ユーザーの詳細ページに投稿一覧を表示する

# やったこと

- タイル表示させる
- ヘッダーのユーザーアイコンに自分のユーザー詳細ページへのリンクを設定してさせる

# 部分テンプレートのcollectionとは?
```ruby
<% @hoges.each do |hoge| %>
  <%= render partial: 'hoge', hoge: hoge %>
<% end %>
```
hogeの要素の数だけ部分テンプレートが繰り返されるが、collectionオプションを使うと、下記のように1行で表せる。
```ruby
<%= render partial: 'hoge', collection: @hoges %>
```
ただし、collectionオプションを使うときは、`partial:`を記述しないとエラーが発生する。

> [【Rails】 部分テンプレートの使い方を徹底解説！ - pikawaka](https://pikawaka.com/rails/partial_template#collectionオプション)

# 疑問点

- 疑問というほどでもないですが 、  

`app/views/posts/_thumbnail_post.html.slim`
```html
.col-md-4.mb-3
  = link_to post_path(thumbnail_post), class: 'thumbs' do
    = image_tag thumbnail_post.images.first.url
```
`humbnail_post.images.first.url`部分において、上の行で画像のリンクを付与しているので末尾の`url`は必要ないような気がしました。(urlを省いても正常に動きました。)

# ちょっと詰まったこと
画像投稿する際に「ファイル選択」のタブを押したが、ダイアログが表示されなくなっり、以前slackのやり取りを思い出しchormeを更新したら直った。

[# times_jiateng
](https://webbeginner2018.slack.com/archives/C02B9PLBXFV/p1640742470011700)