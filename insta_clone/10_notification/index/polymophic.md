# ポリモーフィックとは?

特定の親モデルを持たずに、いろいろな親モデルを持つことができる関連付けの仕組みをポリモーフィックと呼ぶ。  

ポリモーフィックとは、ダックタイピングの一つでオブジェクト指向を実現する方法である。

> 境界の外からそのクラスを触る場合、それの詳細に立ち入らずにクラス自身の持っている情報に判断させるのが良い。  
>
> [そろそろポリモーフィック関連について一言いっとくか - qiita](https://qiita.com/joker1007/items/9da1e279424554df7bb8#comments)

# DBでポリモーフィック関連を理解する

### ポリモーフィック関連

[![Image from Gyazo](https://i.gyazo.com/0048e5f095d4049b3d06492863902aad.png)](https://gyazo.com/0048e5f095d4049b3d06492863902aad)

[![Image from Gyazo](https://i.gyazo.com/7a8569d1613a593ea24c58f4a816a6b9.png)](https://gyazo.com/7a8569d1613a593ea24c58f4a816a6b9)

`comments.target_table`に関連する対象のテーブル名(articles or photos)  
`comments.target_id`に関連する対象のレコードのIDを格納する。  

しかし、以上の設計はSQLのアンチパターンである。なぜかというと、外部キーの設定ができないためcommentsに紐づく対象を保証できない(参照先に絶対レコードがあるという制約)。

### 複数の関連テーブル

[![Image from Gyazo](https://i.gyazo.com/2bf6c09ff78d07a880267ffba7729f07.png)](https://gyazo.com/2bf6c09ff78d07a880267ffba7729f07)

[![Image from Gyazo](https://i.gyazo.com/580706592252a5d46570155a5d0fdf57.png)](https://gyazo.com/580706592252a5d46570155a5d0fdf57)

一つのコメントがarticleとphotoの両方に対して紐付かないよう制約をかけることができないが、データの整合性は担保される。

### その他

他のパターンは[こちら](https://spice-factory.co.jp/development/has-and-belongs-to-many-table/)を参照

# 実装

1. activityモデルを作成する

```ruby
class CreateActivities < ActiveRecord::Migration[5.2]
  def change
    create_table :activities do |t|
     
      t.references :subject, polymorphic: true
      t.references :user, foreign_key: true
      t.integer :action_type, null: false
      t.boolean :read, null: false, default: false

      t.timestamps
    end
  end
end
```
`polymorphic: true`オプションによって、ポリモーフィック関連付けできる。  
`action_type`と`read`カラムには**enum**を使って定数の値を入れたいので、型を指定する。  

また、`t.references :subject, polymorphic: true`によって
```ruby
t.string "subject_type"
t.bigint "subject_id"
```
が生成される。

2.activityモデルの関連付け  
まず、子モデルをポリモーフィック関連付けを定義する。
```ruby
class Activity < ApplicationRecord

  belongs_to :subject, polymorphic: true
  belongs_to :user

  enum action_type: { commented_to_own_post: 0, liked_to_own_post: 1, followed_me: 2 }
end
```
`belongs_to :subject, polymorphic: true`でポリモーフィック関連付けでき、`activity.subject`によってオブジェクトを取得できる。  
またこの際、subjectのオブジェクトのクラスを気にする必要がない。  

次に、`has_one :activity, as: :subject`で親モデルにもポリモーフィック関連付けを定義する。  
(models/comment.rb)
```ruby
class Comment < ApplicationRecord
  has_one :activity, as: :subject, dependent: :destroy
  
  aftet_create_commit :create_activities
  
  private
  
  def create_activities
    Activity.create(subject: self, user: self.post.user, action_type: :commented_to_own_post)
  end
end
```
(models/like.rb)
```ruby
class Like < ApplicationRecord
    has_one :activity, as: :subject, dependent: :destroy
    
    aftet_create_commit :create_activities
  
  private
  
  def create_activities
    Activity.create(subject: self, user: self.post.user, action_type: :liked_to_own_post)
  end

end
```
(models/relationship.rb)
```ruby
class Relationship < ApplicationRecord
    has_one :activity, as: :subject, dependent: :destroy
    
    aftet_create_commit :create_activities
  
  private
  
  def create_activities
    Activity.create(subject: self, user: self.followed, action_type: :followed_me)
  end

end
```

3.ビューの実装  
(app/views/shared/_header.html.slim)
```slim
= render 'shared/header_activities'
```
ヘッダーから`header_activiry`を返す。

(app/views/shared/_header_activities)
```slim
- if current_user.activities.present?
  - current_user.activities.each do |activity|
    = render "shared/#{activity.action_type}", activity: activity
- else
  .dropdown-item
    | お知らせはありません 
```
`= render "shared/#{activity.action_type}"`のおいて、`action_type`ごとに条件分けしておくことで、テンプレート先のactivityオブジェクトにどのメソッドを使えばいいか迷わなくなる。

# 参考

[Raild ガイド - ポリモーフィック関連付け](https://railsguides.jp/association_basics.html#ポリモーフィック関連付け)

[複数のテーブルに対して多対一で紐づくテーブルの設計アプローチ](https://spice-factory.co.jp/development/has-and-belongs-to-many-table/)

[SQLアンチパターンを読んで （ポリモーフィック関連について）](https://blog.motimotilab.com/?p=207)

[ポリモーフィック関連のコントローラー - 猫rails](https://nekorails.hatenablog.com/entry/2019/06/13/031003)

[Railsのポリモーフィック関連とはなんなのか - qiita](https://qiita.com/itkrt2y/items/32ad1512fce1bf90c20b)

[【Rails】ActiveRecord：単一テーブル継承(sti)とポリモーフィック関連を未だにぱっと思い出せないのでまとめ。
](https://shirusu-ni-tarazu.hatenablog.jp/entry/2012/11/04/173742)

[ポリモーフィックでコメントを実装する](https://skillhub.jp/courses/145/lessons/1006)