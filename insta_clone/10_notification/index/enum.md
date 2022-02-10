# enumとは?

1つのカラムに指定した複数個の定数を保存できるようにするためのモノ

このenumを使用すると指定した複数個の定数以外は保存できなくなる。  
また、カラムに指定した定数が入っているレコードを取り出すのが用意になる。

```ruby
# 定義
enum blood_type: { A: 0, B: 1, O: 2, AB: 3 }
```

```azure
# 複数個の定数リスト
User.blood_types
=> {"A"=>0, "B"=>1, "O"=>2, "AB"=>3}

# Userインスタンスのenumカラムの定数を表示
User.find_by(blood_type: 'A').blood_type
=> "A"
```

# tableにenum用のカラムを用意

enumに指定するカラムの型は、integer型 か boolean型である。  
integer型・・・**整数(0,1,2など)**と2個以上の定数  
boolean型・・・**真偽値(true, false)**と2個の定数  
といった形でenumはDBに保存される。

```azure
class CreateUsers < ActiveRecord::Migration[5.2]
  def change
    create_table :users do |t|
      t.string     :name,           null: false, default: ""
      t.integer   :age,              null: false
      # 新しくenum用のinteger型のblood_typeカラムを追加
      t.integer   :blood_type, null: false, default: 0
      t.timestamps
      t.timestamps
    end
  end
end
```

# モデルの定義

#### integer型の場合

enumはハッシュで複数個の定数を定義できるので、定数の数だけhashの要素を保存できる。  
```azure
class User < ApplicationRecord
  enum blood_type: { A: 0, B: 1, O: 2, AB: 3 }
end
```
しかし、テーブルの型定義では blood_type をinteger型で定義していたので、血液型の文字列をDBに保存するのではなく、**hashのkeyに対応するvalueの整数が保存される**。  

[![Image from Gyazo](https://i.gyazo.com/7dd497ffa1fc1df4a1d1f36ce726cb0e.png)](https://gyazo.com/7dd497ffa1fc1df4a1d1f36ce726cb0e)

###### 配列での定義方法

```azure
class User < ApplicationRecord
  # シンボルで定義する場合
  enum blood_type: [ :A, :B, :O, :AB ]

  # 文字列で定義する場合
  enum blood_type: [ "A", "B", "O", "AB" ]
end
```
配列定義の場合、

1. シンボルが文字列を定義する
2. 配列の添字と要素の定数が紐づく

配列のインデックスは、先頭から0が入って定数と紐づくので**DBには数値が保存される**。

- User.create(blood_type: 'A') → DBに 0 が保存される 
- User.create(blood_type: 'B') → DBに 1 が保存される
- User.create(blood_type: 'O') → DBに 2 が保存される
- User.create(blood_type: 'AB') → DBに 3 が保存される

#### boolean型の場合

boolean型の場合、DBにはinteger型と同じように数値が保存される。

[![Image from Gyazo](https://i.gyazo.com/6a7af65d0e186f159d14a41baaaa5f6d.png)](https://gyazo.com/6a7af65d0e186f159d14a41baaaa5f6d)

しかし、boolean型のカラムの場合、enum をあまり実装しない。  
boolean型のカラムを作成した時二択しかないので、enumを設定しなくてもbooleanだけで十分機能を実装できる。

# 便利なメソッド

#### 確認メソッド

enumには確認メソッドがあり、今enumカラム(blood_type)に入っている定数が何なのか確認する。

```ruby
user = User.find_by(name: 'programan')
=> #<User:0x007f82b7b6fe40
  id: 1,
  name: "programan",
  age: 25,
  blood_type: "A",
  is_married: false,
  created_at: Wed, 29 Jan 2020 01:44:45 UTC +00:00,
  updated_at: Wed, 29 Jan 2020 01:44:45 UTC +00:00>

user.blood_type
=> "A"

user.A?
=> true
user.B?
=> false
user.O?
=> false
user.AB?
=> false

user.C?
NoMethodError: undefined method `C?' for #<User:0x007f82b7b6fe40>
```

# 参考

[Railsガイド - enum](https://railsguides.jp/active_record_querying.html)

[ActiveRecord::Enum](https://api.rubyonrails.org/v7.0/classes/ActiveRecord/Enum.html)

[【Rails】 enumチュートリアル - pikawaka](https://pikawaka.com/rails/enum)
