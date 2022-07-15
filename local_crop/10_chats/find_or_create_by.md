# find_or_create_byメソッド

条件を指定して初めの1件を取得し1件もなければ作成する。

# 使い方

```ruby
モデル.find_or_create_by(条件, ブロック引数)

# 失敗したら例外発生
モデル.find_or_create_by!(条件, ブロック引数)
```

# 実装例

存在しないので新しく作成
```ruby
User.find_or_create_by(first_name: "Taraou")
#=> <User id: 1, first_name: "Tarou", last_name: nil>
```

既に存在するのでレコードを取得
```ruby
User.find_or_create_by(first_name: "Taraou")
#=> <User id: 1, first_name: "Taraou", last_name: nil>
```

# 参考

[新しいオブジェクトを検索またはビルドする - Railsガイド](https://railsguides.jp/active_record_querying.html#%E6%96%B0%E3%81%97%E3%81%84%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%82%92%E6%A4%9C%E7%B4%A2%E3%81%BE%E3%81%9F%E3%81%AF%E3%83%93%E3%83%AB%E3%83%89%E3%81%99%E3%82%8B)

[Railsドキュメント](https://railsdoc.com/page/find_or_create_by)