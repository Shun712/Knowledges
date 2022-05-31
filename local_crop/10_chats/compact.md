# compactメソッド

要素が`nil`のものを取り除く

# 実行例

```ruby
Arrayオブジェクト.compact
```

```ruby
ary = [1, 2, nil, 3, 4, nil]
newary = ary.compact
p ary
p newary

=> [1, 2, nil, 3, 4, nil]
=> [1, 2, 3, 4]
```

```ruby
ary = [1, 2, 3, nil, 4, nil]
ary.compact!
p ary

=> [1, 2, 3, 4]
```

# 参考

[Array#compact (Ruby 3.1 リファレンスマニュアル)](https://docs.ruby-lang.org/ja/latest/method/Array/i/compact.html)

[要素が「nil」のものを取り除く](https://www.javadrive.jp/ruby/array_class/index9.html)