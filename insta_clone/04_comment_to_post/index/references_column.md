# 外部キーのreference型カラム

Railsのマイグレーション機能で、`reference`は簡単にリレーション用のカラムを追加することができる。

UserモデルとPostモデルがあると仮定する。
```ruby
class User < ApplicationRecord
  has_many :posts
end
```
```ruby
class Post < ApplicationRecord
  belongs_to :user
end
```
`$ rails g model post user:references body:text`
```ruby
def change
  create_table :posts do |t|
    t.references :user
    t.text :body    # 記事本文
  end
end
```

これで`migrate`すると、postsテーブルに`user_id`カラムが追加される。

`references` と使った場合は追加した `user_id` カラムに対して index を自動で作ってくれる。

> [DBのインデックスと複合インデックス - qiita](https://qiita.com/towtow/items/4089dad004b7c25985e3)

ちなみにもう一つ方法があり、`user_id`カラムが追加されるので、**`user_id`を明記しておくのとほぼ同じである**。

```ruby
def change
  create_table :posts do |t|
    t.text :body    # 記事本文
    t.integer :user_id, index :true ← どちらか追加
  end
  add_index :posts, :user_id ← どちらか追加
end
```
**こちらは、`index` を自分で追加しないといけない。**

## referenceの他の仕組み

`references`には、オプションで`foreign_key`の指定がある。
`t.references :user, foreign_key: true`

> 外部キー制約はRails の機能というよりは MySQL や PostgreSQL といったデータベース側の機能で、外部キー制約を使うことで、データの構造をより厳格にすることができるようになるので、こうしたリレーションをさせるための id に対しては基本的にはつけた方が良いです。

> [Rails の マイグレーションと references について](https://menta.work/post/detail/2656/PVcqTLbkKeje8bgdkncG)

ただし、外部キー制約があると困る場面がある。  
例えば、ユーザーがした投稿は、ユーザーが退会してもそのまま残したいという場合に、

```ruby
def change
  create_table :posts do |t|
    t.references :user, foreign_key: true
    t.text :body
  end
end
```
外部キー制約をつけたので、`posts` テーブルの `user_id` のユーザーは必ずデータとして存在しなければならない。

そんな中ユーザーが退会して `users` テーブルのデータを消そうとすると、外部キー制約で投稿を削除できないエラーが発生する。

エラーにならないようにするために、`user` を消す前に `user` にひもづく `post` を全て消さなければならない。

そうすると、退会したユーザーの投稿は残らなくなってしまう。

こうした場合は、**外部キー制約をつけてはならない。**

## カラム追加時

クラス名は、`AddUserRefToProducts` だと  
何のカラム名が どの型で どのテーブルに 追加されたという名前になるので
わかりやすい。

## 外部キーにnullが入ることを許容する

外部キーとして設けたカラムに`null`を許容されるオプションは、`optional: true`をつける。

```ruby
class Question < ApplicationRecord
  belongs_to :user, optional: true
end
```

# 参考

[Railsの外部キー制約とreference型について - qiita](https://qiita.com/ryouzi/items/2682e7e8a86fd2b1ae47)

[外部キーをreferences型カラムで保存する - qiita](https://qiita.com/sinagaki58/items/7edea51ef00e393834ca)

[Rails の マイグレーションと references について](https://menta.work/post/detail/2656/PVcqTLbkKeje8bgdkncG)

[【Rails】references型について - qiita](https://qiita.com/mmaumtjgj/items/cdc76572d392957c4299)

[【Rails】後からカラムを追加して外部キーを張る際に、add_referenceを使う場合の注意点。 - qiita](https://qiita.com/kurawo___D/items/e3694f7a870a1cc4738e)

[外部キーにnullが入ることを許容する[Rails] - qiita](https://qiita.com/takuyanin/items/6f6be86d1265be21bf9e)