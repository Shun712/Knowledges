# UserとUserの多対多(M:N)を設計
多対多で関連しているため、中間テーブルが存在する。
関連を表現しているため、Relationshipモデルと名付ける。
中間テーブルなので、各親テーブルの`primary_key`を`foreign_key`として保存する。

[![Image from Gyazo](https://i.gyazo.com/50cc31731cf6dd8217c1ce0e0c414ef4.png)](https://gyazo.com/50cc31731cf6dd8217c1ce0e0c414ef4)

これをUserモデルに直すと、
・フォローする側(`follower`)のUserから見て、フォローされる側(`followed`)のUserを（中間テーブルを介して）集める
・フォローされる側(`followed`)のUserから見て、フォローしてくる側(`follower`)のUserを（中間テーブルを介して）集める

| id | follower_id | followed_id |
|:---------:|:----------:|:------------:|
| 1   |  1 | 2   |
| 2   |  1  | 3    |
| 3   |  2  | 1    |

#### 1. 設計通りに下準備
データベースを設定する。
```ruby
class CreateRelationships < ActiveRecord::Migration[5.2]
  def change
    create_table :relationships do |t|
      t.integer :follower_id, null: false
      t.integer :followed_id, null: false

      t.timestamps
    end
    # フォローするユーザー・フォローされるユーザーのidについて、indexを貼る（パフォーマンス向上のため）
    add_index :relationships, :follower_id
    add_index :relationships, :followed_id
    # フォロー関係がダブらないように、ユニーク制約をつける
    add_index :relationships, [:follower_id, :followed_id], unique: true
  end
end
```
ルーティングを設定する。
```ruby
  resources :relationships, only: %i[create destroy]
```

#### 2. アソシエーションの記述
`class_name`というオプションを使えば、Userモデルを**Followerモデル**や**Followedモデルとモデル名を擬似的に作り出すことができる**。
`foreign_key`は、 参照先のテーブルの外部キーのカラム名を指定できる。つまり、親の`primary_key`を指定してあげれば、「フォローする側(follower)のUserからみた」と言う情報も取得することができる。
(app/models/user.rb)
```ruby
  # foreign_keyで定義することで、親モデル(follower)と関連付けられる。
  has_many :active_relationships, class_name: 'Relationship', foreign_key: 'follower_id', dependent: :destroy

  # foreign_keyで定義することで、親モデル(followed)と関連付けられる。
  has_many :passive_relationships, class_name: 'Relationship', foreign_key: 'followed_id', dependent: :destroy

  # フォローされる側(followed)のユーザーを中間テーブル(active_relationships)を介して取得することを「following」と定義
  has_many :following, through: :active_relationships, source: :followed

  # フォローする側(follower)のユーザーを中間テーブル(passive_relationships)を介して取得することを「followers」と定義
  has_many :followers, through: :passive_relationships, source: :follower
```
(app/models/relationship.rb)
```ruby
class Relationship < ApplicationRecord
  belongs_to :follower, class_name: 'User'
  belongs_to :followed, class_name: 'User'
  validates :follower_id, presence: true
  validates :followed_id, presence: true
  validates :follower_id, uniqueness: { scope: :followed_id }
end
```
`has_many :active_relationships, class_name: 'Relationship', foreign_key: 'follower_id', dependent: :destroy`  
までで実装したassociationのみだと、紐づくidしか取得できず、ユーザー名を取得することができない。
そこで、  
`has_many :following, through: :active_relationships, source: :followed`  
と記述する必要が出てくる。

#### 3. コントローラーの実装
(app/controllers/relationships_controller.rb)
```ruby
class RelationshipsController < ApplicationController

  def create
    # ビューのクエリパラメータから:followed_idを取得
    @user = User.find(params[:followed_id])
    current_user.follow(@user)
  end

  def destroy
    # Relationshipはfollowedとfollowerが一意なのでパラメーターからidを取得
    # followedは、belongs_toでfollowedを関連付けしているので、.followedでユーザーを取ってこれる。
    @user = Relationship.find(params[:id]).followed
    current_user.unfollow(@user)
  end
end
```
ファットコントローラーにならないために、Userモデルにフォロー、アンフォローメソッドを定義
(app/models/user.rb)
```ruby
  def follow(other_user)
    following << other_user
  end

  def unfollow(other_user)
    following.destroy(other_user)
  end

  def following?(other_user)
    following.include?(other_user)
  end

  def feed
    # 自分と自分のフォローしているユーザーだけフィードに表示するよう
    Post.where(user_id: following_ids << id)
  end
```

#### 4. ビューの実装
コメント機能のでAjaxの実装と被るので割愛。

# 参考
[【初心者向け】丁寧すぎるRails『アソシエーション』チュートリアル【幾ら何でも】【完璧にわかる】 - qiita](https://qiita.com/kazukimatsumoto/items/14bdff681ec5ddac26d1#%E3%81%8A%E6%B0%97%E3%81%AB%E5%85%A5%E3%82%8A%E6%A9%9F%E8%83%BD%E3%82%92er%E5%9B%B3%E3%82%92%E4%BD%BF%E3%81%A3%E3%81%A6%E8%A8%AD%E8%A8%88%E3%81%97%E3%82%88%E3%81%86)

[Railsドキュメント - has_many](https://railsdoc.com/page/has_many)