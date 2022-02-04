# モデルのscopeとは?

- scopeは、関連オブジェクトやモデルへのメソッド呼び出しとして参照される。  

- scopeでは、`where`、`joins`、`includes`などのメソッドを使用できる。  

- どのscopeメソッドも、常にActiveRecord::Relationオブジェクトを返す。

- 単純なscopeを設定するには、クラスの内部でscopeメソッドを使用する。

# モデルのscopeを利用するメリット

- モデルのscopeを定義することで、複数のクエリを一つのメソッドとしてまとめる。

- コントローラーで複数のクエリを書くよりも、scopeを使って可読性が上がる。

# scopeを使わない場合

以下の例は、whereやorderのクエリメソッドが連結しているため、読みづらくなっている。

```ruby
class UsersController < ApplicationController
  ...
  def index
    @users = User.where(deleted: false).order(created_at: :desc)
  end
  ...
end
```

# scopeを使う場合
scopeは再利用可能なので、繰り返し何度も呼び出す際はscopeで定義したほうがコードも簡略化できる。

```ruby
class User < ApplicationRecord
  ...
    # deletedカラムがfalseであるものを取得する
    scope :active, -> { where(deleted: false) }
    # created_atカラムを降順で取得する
    scope :sorted, -> { order(created_at: :desc) }
    # activeとsortedを合わせたもの
    scope :recent, -> { active.sorted }
  ...
end
```

```ruby
class UsersController < ApplicationController
  ...
  def index
    # scope recentを定義しなかった場合
    @users = User.where(deleted: false).order(created_at: :desc)
    # scope recentを定義した場合
    @users = User.recent
  end
  ...
end
```

# 参考
[Raisガイド - スコープ](https://railsguides.jp/active_record_querying.html#%E3%82%B9%E3%82%B3%E3%83%BC%E3%83%97)

[Railsのモデルのscopeを理解しよう - qiita](https://qiita.com/ozin/items/24d1b220a002004a6351)