# 中間テーブルの作成（多対多(M:N)を設計）
多対多をプログラミングで実装するには、お互いのidだけを保存する中間テーブルが必要になる。
つまり、`post_id`と`user_id`でその組み合わせが`id`として中間テーブル(`likesテーブル`)に保存される。

### 1.  Likeモデルとassociationを設定
中間テーブルはたくさん持たれる側なので、外部キーを2つ指定する形になるので、
`belongs_to :user`と`belongs_to :post`を設定する。
```ruby
class Like < ApplicationRecord
  belongs_to :user
  belongs_to :post
end
```

```ruby
class CreateLikes < ActiveRecord::Migration[5.2]
  def change
    create_table :likes do |t|
      t.references :user, foreign_key: true
      t.references :post, foreign_key: true

      t.timestamps
      # この設定で、「いいね」が2回以上保存されるのを制限
      t.index [:user_id, :post_id], unique: true
    end
  end
end
```
```ruby
class User < ApplicationRecord
.
.
.
  has_many :likes, dependent: :destroy
  # ユーザーがいいねしたツイートを直接アソシエーションで取得することができるようカラムを設定
  has_many :like_posts, through: :likes, source: :post
```
`has_many through`で取得したいモデル(post)を指定できる。
`source`は「参照元のモデル」を指すオプション。
これを指定することで**アソシエーションでメソッドチェーンする時の名称を変更**することができる。
本当は、`has_many :posts, through: :likes`としたいところだが、すでに`has_many :posts`を定義しているので、名称を変更している。

Postも同様に設定する。

### 2. Likeモデルに適切なバリテーションを設定
```ruby
class Like < ApplicationRecord
  belongs_to :user
  belongs_to :post

  validates :user_id, uniqueness: { scope: :post_id }
end
```

バリテーションでは、各postは同じuserに「いいね」されないようにLikeモデルのuserカラムに一意性制約をつけている。

### 3. like, unlike, like?のモデルメソッドを定義
```ruby
  # 「いいね」したpostをlike_postsへpush
  def like(post)
    like_posts << post
  end
  
  # 「いいね」したpostをlike_postsから削除
  def unlike(post)
    like_posts.destroy(post)
  end

  # userがすでにそのpostに「いいね！」しているかを判別
  def like?(post)
    like_posts.include?(post)
  end
```
これらのメソッドをビューで使うため、可読性向上を目的としてモデルに定義している。

### 4. ビューの実装
Ajaxの実装と同様の内容なので割愛。

### 5. コントローラーの実装
```ruby
def create
    @post = Post.find(params[:post_id])
    current_user.like(@post)
  end

  def destroy
    @post = Like.find(params[:id]).post
    current_user.unlike(@post)
  end
```
createアクションでは、該当の投稿を@postに格納し、current_userが所有する`like_posts`に@postを追加する。
逆にdestroyアクションにおいては「いいね」した該当の投稿を@postに格納し、current_userが所有する`like_posts`から@postを削除する。

# 参考

[【初心者向け】丁寧すぎるRails『アソシエーション』チュートリアル【幾ら何でも】【完璧にわかる】 - qiita](https://qiita.com/kazukimatsumoto/items/14bdff681ec5ddac26d1)

[Railsで remote: true と js.erbを使って簡単にAjax(非同期通信)を実装しよう！(いいね機能のデモ付) - qiita](https://qiita.com/motoki0208/items/45211df065e0c037d032)

[RailsでAjaxで「いいね！」機能を実装する - qiita](https://qiita.com/tanutanu/items/b435af08aff706e01f2a)