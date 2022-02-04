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

# 参考

> [Railsガイド - 3.4 パーシャルを使う](https://railsguides.jp/layouts_and_rendering.html#%E3%82%B3%E3%83%AC%E3%82%AF%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%92%E3%83%AC%E3%83%B3%E3%83%80%E3%83%AA%E3%83%B3%E3%82%B0%E3%81%99%E3%82%8B)

> [【Rails】 部分テンプレートの使い方を徹底解説！ - pikawaka](https://pikawaka.com/rails/partial_template#collectionオプション)