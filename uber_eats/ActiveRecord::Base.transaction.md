# transaction の目的

>・データベース内の情報の整合性を保つための手段  
>・複数のデータベースにまたがる分散トランザクションはサポートしていない  
>・使用するにはデータベースがトランザクションをサポートしていることが必要

> 引用:[トランザクション - Railsドキュメント](https://railsdoc.com/page/transaction)

複数のSQL文に対して、すべてのアクションが成功した際にDBの変更を発生させるという条件を守らせるのに使用する。  
例えば、  
1. 本を100円で購入
2. 本のデータを保存
3. 残高の保存
という処理でどこが一つ失敗して、本の保存だけできなかった場合、データの整合性に不具合が生じる。

```ruby
この中のどれか一つでも例外が発生するちrollbackしてくれる！
ActiveRecord::Base.transaction do
  book.buy(100) #　本を100円で買うメソッド
  book.save!    #　上記の本の情報が登録される処理
  balance.save! #　自分の残高の保存
end
```

# Transactionのrollbackが発生する条件

`rollback`が発生するには、「例外」が必要となる。  
`save`に`!`をつけると、失敗したら例外を吐く。`transaction`を使うときは、`save`ではなく`save!`、`destroy`ではなく`destroy!`を使うと`transaction`がちゃんと拾ってくれる。  
`!`をつけないと不整合なデータが保存validationの網をかいくぐって保存されてしまう可能性もあります。

```ruby
ActiveRecord::Base.transaction do
  david.update_attributes!(:amount => -100)
  mary.update_attributes!(:amount => 100)
end
```
※ただし、rails6.1以降は`update_attributes!`は非推奨。updateを使うように！

# さらに具体例

`find_by`メソッドの結果が`nil`であった場合変数davidに`nil`が代入され、条件分岐をスルーしてしまうので、この例外をキャッチし処理をするコードを準備する必要がある。

```ruby
ActiveRecord::Base.transaction do
  david = User.find_by_name("david")
  raise ActiveRecord::RecordNotFound if david.nil?
  if(david.id != john.id)
    john.update_attributes!(:amount => -100)
    mary.update_attributes!(:amount => 100)
  end
end
```

# 参考

[RailsのTransactionの使い方について - qiita](https://qiita.com/pandama09396862/items/5bc9bd265009982dd3f5)

[Rails トランザクションの挙動・注意点について](https://zenn.dev/neko_engineer/articles/fe8c19d5c26763)