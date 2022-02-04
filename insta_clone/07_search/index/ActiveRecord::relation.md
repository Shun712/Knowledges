# ActiveRecordとは?

- DBにクエリを発行する

- 様々なDBとの互換性がある

- DBの種類に関わらず、同じ表記ができる

# ActiveRecordの各検索メソッドのリクエストタイミング

メソッドは大きく、2種類に分かれる

### 1. DBへのクエリが発生するメソッド
`ActiveRecord::FinderMethods`に実装されているメソッドがこれにあたる。

> [ActiveRecord::FinderMethods](https://api.rubyonrails.org/classes/ActiveRecord/FinderMethods.html)

`find, find_by, take, first, last, exists?`  

すぐにクエリを発行してDBにアクセスし、レコード（Modelのインスタンス or インスタンスの配列）を返す。


### 2. DBへのクエリが発生せず、ActiveRecord::Relationのオブジェクトを返すメソッド
`where、limit`など  

`ActiveRelation`のオブジェクトを返し、実際にデータが入るタイミング(ビューに表示)までDBにアクセスしない（遅延評価）。


# ActiveRecord::Relationとは?
クエリを生成するための情報を保持し、メソッドチェーンでつなげることができるため、再利用性が高い。  

`ActiveRecord::Relation`は形が配列に似ているが配列とは異なる。
```ruby
AdminUser.where(id: [2, 3]).class
=> AdminUser::ActiveRecord_Relation
```

```ruby
AdminUser.where(id: [2, 3]).select(&:name).class
=> Array
```

# 参考

[Railsで配列をActive Record Relationに変換したい - qiita](https://qiita.com/fgem28/items/25e25d400f2ce21f4235)

[ActiveRecord各メソッドのクエリ実行タイミングについて - qiita](https://qiita.com/ykamez/items/0c81a33ec1b90219d541)

[【続・find と where の違い 】ActiveRecord::Relation を学ぶ。 - qiita](https://qiita.com/7coco/items/2e3a9e720d29791f1cfc)

[ActiveRecord::Relationのメソッドが何を返すのか - qiita](https://qiita.com/kichion/items/a1539fcb124b69c765bf)

[Railsガイド - collection.where(...)](https://railsguides.jp/association_basics.html#has-many%E3%81%A7%E8%BF%BD%E5%8A%A0%E3%81%95%E3%82%8C%E3%82%8B%E3%83%A1%E3%82%BD%E3%83%83%E3%83%89-collection-where)