# 配列をActiveRecord::Relationで再取得する

Rubyなどで使える`map、reject、select`などのメソッドはとても便利だが、Railsの`all`メソッドで取得すると、Arrayクラスとなる。

```ruby
[2] pry(main)> User.all.class
=> User::ActiveRecord_Relation

[4] pry(main)> User.all.map{|user| user }.class
  User Load (0.5ms)  SELECT "users".* FROM "users"
=> Array
```

# map、reject、selectを使,
ActiveRecord::Relationで取得する

```ruby
@susers = User.where(id: users.map{ |user| user.id })
```

# 参考

[配列をActiveRecord::Relationで再取得するメソッドを作ってみる - qiita](https://qiita.com/shibadai/items/ddbc76a8b980cd8354bc)