# RSpecのテスト中にMySQL client is not connected

システムスペックを実行していると以下のエラーが発生した。

```ruby
Failure/Error: _query(sql, @query_options.merge(options))

ActiveRecord::StatementInvalid:
  Mysql2::Error: MySQL client is not connected
```

MySQLクライアントとの接続が確立できていないらしい。  

# 仮設

FactoryBotのインスタンス生成の記述を増やしたタイミングでエラーがエラーが発生しはじめたため、ここで負荷がかかって処理が止まった可能性がある。

# 対応策

```ruby
# config/environments/test.rb

Rails.application.configure do
  config.active_job.queue_adapter = :inline
# 省略
end
```

# 参考

[RSpecのテスト中にMySQL client is not connected - qiita](https://qiita.com/shun915a/items/e18f538be6221f929876)