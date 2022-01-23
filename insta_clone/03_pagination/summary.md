# 03 ページネーションの実装

## やったこと

- ページネーションにはkaminariを使用する
- 1ページあたり15件とする
- ページネーションにもbootstrapを適用する

## kaminarとは?

rubyのgemの一つでページネーションを簡単に実装するためのもの。
例えば、投稿一覧がトップページに表示されるサイトの場合、全ての投稿がトップページに表示されると読み込むまでに時間がかかりる上に、かなり読みにくくなる。
また、Railsのパフォーマンスも低下してしまう。

> [kaminariとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/03_pagination/index/kaminari.md)

## 学んだこと

- kaminariはQAアプリで実装済みなので理解が早かった。もう少し、深堀りして実行したコマンドを調べてみた。

`rails g kaminari:views bootstrap4`
bootstrapのフレームワークを取り入れたビューファイル(slimで実装していたらslim形式で)が作成される。


`rails g kaminari:config`
`config/initializers/kaminari_config.rb`が作成され、このファイルに表示件数など設定できる。


- N + 1問題を復習してみる

`post`の`index`ページでは`post.user.username`と`Post`デーブルへのアクセスが1回、`post.user`では`User`テーブルへのアクセスが5回だけ、SQLが発行される問題が起こっている。

まず、`index`アクションに`includes`メソッドを入れないパターンのクエリは計6回
```
Rendering posts/index.html.slim within layouts/application
  Post Load (1.4ms)  SELECT  `posts`.* FROM `posts` ORDER BY `posts`.`created_at` DESC LIMIT 5 OFFSET 0
  ↳ app/views/posts/index.html.slim:4
  User Load (0.2ms)  SELECT  `users`.* FROM `users` WHERE `users`.`id` = 10 LIMIT 1
  ↳ app/views/posts/_post.html.slim:5
  User Load (0.2ms)  SELECT  `users`.* FROM `users` WHERE `users`.`id` = 9 LIMIT 1
  ↳ app/views/posts/_post.html.slim:5
  User Load (0.2ms)  SELECT  `users`.* FROM `users` WHERE `users`.`id` = 8 LIMIT 1
  ↳ app/views/posts/_post.html.slim:5
  User Load (0.2ms)  SELECT  `users`.* FROM `users` WHERE `users`.`id` = 7 LIMIT 1
  ↳ app/views/posts/_post.html.slim:5
  User Load (0.2ms)  SELECT  `users`.* FROM `users` WHERE `users`.`id` = 6 LIMIT 1
```
次に、`includes`メソッドを入れるパターンのクエリは計2回
```
Rendering posts/index.html.slim within layouts/application
  Post Load (1.3ms)  SELECT  `posts`.* FROM `posts` ORDER BY `posts`.`created_at` DESC LIMIT 5 OFFSET 5
  ↳ app/views/posts/index.html.slim:4
  User Load (0.3ms)  SELECT `users`.* FROM `users` WHERE `users`.`id` IN (5, 4, 3, 2, 1)
  ↳ app/views/posts/index.html.slim:4
```

ユーザーの数が増えるとさらにクエリの発行が多くなるので、N + 1問題はつねに注意しておきたい。