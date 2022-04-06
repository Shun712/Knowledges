# tryメソッドとは?

「**オブジェクトがnilでない場合のみ**、そのオブジェクトのメソッドを実行する。」メソッドである。

# tryメソッドを使うケース

1. 指定した**メソッドがない**場合、エラー発生させない
2. tryメソッドを実行する**オブジェクトがnil**だった場合、エラー発生させない

```ruby
User.find_by('name like ?', '%hogehoge%')
=> nil
User.find_by('name like ?', '%hogehoge%').try(:email)
=> nil
```

# 関連するメソッド

&.(ボッチ演算子)

# 参考

[【Rails】 ｢tryメソッド｣｢try!メソッド｣｢&.演算子｣の違いとは？ - pikawaka](https://pikawaka.com/rails/try)

[Railsでよく使う、tryメソッドの使い方をまとめてみた - qiita](https://qiita.com/ngron/items/ec5f72639634949c126e)