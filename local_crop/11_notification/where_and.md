# whereメソッドでandの絞り込み

復数カラム指定でAND検索をすると、どちらの条件にも当てはまるレコードを取得できる。

# シンボルの場合

```ruby
User.where(name: "太郎", age: 25)

# 発行されるSQL
User Load (2.3ms)  SELECT `users`.* FROM `users` WHERE `users`.`name` = '太郎' AND `users`.`age` = 25
=> [#<User:0x007fd316e2ecf8
  id: 3,
  name: "太郎",
  age: 25,
  height: nil,
  weight: 22>]
```

# 文字列の場合

文字列で指定する際は`?`(プレースホルダー)で指定できる。

```ruby
User.where("name = ? and age = ?", "太郎", 25)

# 発行されるSQL
User Load (0.6ms)  SELECT `users`.* FROM `users` WHERE (name = '太郎' and age = 25)
=> [#<User:0x007fd316e2ecf8
  id: 3,
  name: "太郎",
  age: 25,
  height: 167,
  weight: 52>]
```

# 参考

[【Rails】 whereメソッドを使って欲しいデータの取得をしよう！ - pikawaka](https://pikawaka.com/rails/where)