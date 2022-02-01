# uniqueness: scope を使ったユニーク制約方法

`uniqueness: scope`はuniqueness制約をかける条件を制限できる。  
以下はコンソールで試したことである。

```
class Like < ApplicationRecord
  belongs_to :user
  belongs_to :post

  validates :user_id, uniqueness: { scope: :post_id }
end
```
バリテーションでは、各postは同じuserに「いいね」されないようにLikeモデルのuserカラムに一意性制約をつけている。

```
[1] pry(main)> post = Post.first

# post に user_id:1 が「いいね」する
[2] pry(main)> post.likes.create(user_id: 1)

   (5.1ms)  COMMIT
 
 # 再び、post に user_id:1 が「いいね」するとロールバックされる
[3] pry(main)> post.likes.create(user_id: 1)

   (0.2ms)  ROLLBACK
 
 # post に user_id:2 が「いいね」する
[4] pry(main)> post.likes.create(user_id: 2)

   (1.4ms)  COMMIT

```

# データベース側での制約

モデルだけでなく、データベース側でも制約を設定する場合は、両方のカラムに`unique`インデックスを作成する。

```
class AddUniqueIndexToLikes < ActiveRecord::Migration
  def change
    add_index :likes, [:user_id, :post_id], unique: true
  end
end
```

# 参考

[Railsガイド - Active Record バリデーション](https://railsguides.jp/active_record_validations.html#uniqueness)

[uniqueness: scope を使ったユニーク制約方法の解説 - qiita](https://qiita.com/j-sunaga/items/d7f0e944baad6e56206c)
