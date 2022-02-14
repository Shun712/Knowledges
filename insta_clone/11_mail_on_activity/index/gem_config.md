# gem configとは？

Ruby on Railsで便利に定数を管理することができるgemである。

# config関連のファイルを生成

|                  config/initializers/config.rb                  |configの設定ファイル|
|:---------------------------------------------------------------:|:-------:|
|                       config/settings.yml                       |すべての環境で利用する定数を定義|
|                    config/settings.local.yml                    |ローカル環境のみで利用する定数を定義|
|                 config/settings/development.yml                 |開発環境のみで利用する定数を定義|
|                 config/settings/production.yml                  |本番環境のみで利用する定数を定義|
|                  config/settings/test.yml                       |テスト環境のみで利用する定数を定義|

以上のファイルが生成され、`.gitignore`に自動で以下が追記される。
```ruby
config/settings.local.yml
config/settings/*.local.yml
config/environments/*.local.yml
```

# 定数を定義する

Yaml形式で書けるので見やすい。

```ruby
default_url_options:
  host: 'localhost:3000'
```

# 参考

[gem configを理解する ~ configを使った定数管理の方法 - qiita](https://qiita.com/tanutanu/items/8d3b06d0d42af114a383)

[【Rails】「config」gemを使って定数管理をおこなう方法](http://vdeep.net/rubyonrails-config-gem)