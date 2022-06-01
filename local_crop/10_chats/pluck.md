# pluckメソッド

引数に指定したカラムの値を配列で返してくれるメソッドである。

# 基本構文

```ruby
モデル名.pluck(:カラム名)

モデル名.all.map(&:カラム名) # 上記と同じ
```

# 実行例

```ruby
Owner.pluck(:name)
SELECT `owners`.`name` FROM `owners`

=> ["田中", "伊藤", "高橋", "加藤"] # 返り値
```

返り値は、`pluck`メソッドの引数に渡したnameカラムの値が配列に格納される。

# 複数の引数

```ruby
Owner.pluck(:id, :name)
SELECT `owners`.`id`, `owners`.`name` FROM `owners`

=> [[1, "田中"], [2, "伊藤"], [3, "高橋"], [4, "加藤"]] # 返り値
```

`pluck`メソッドの引数に渡したidカラムとnameカラムの値が、**二次元配列**に格納される。

# 条件を指定

```ruby
Owner.where('age <= 60').pluck(:id)
SELECT `owners`.`id` FROM `owners` WHERE (age <= 60)

=> [1, 2, 4] # 返り値
```

# 参考

[Railsドキュメント](https://railsdoc.com/page/model_pluck)

[【Rails】 便利なpluckメソッドの使い方をマスターしよう！ - pikawaka](https://pikawaka.com/rails/pluck)