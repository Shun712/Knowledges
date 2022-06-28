# geokit-railsを導入

このgemを導入することで、座標データを持つモデルからレコードを取得できる。

```ruby
gem 'geokit-rails'

$ bundle install

$ rails g geokit_rails:install
```

# 座標データを持つモデルにオプションを設定

```ruby
class Location < ActiveRecord::Base
  acts_as_mappable :default_units => :miles,
                   :default_formula => :sphere,
                   :distance_field_name => :distance,
                   :lat_column_name => :lat,
                   :lng_column_name => :lng
end
```

# 具体例

いろいろなAPIが用意されており、以下は5マイル以内のLocationを取得している。

```ruby
Location.within(5, :origin => @somewhere)
```

# 参考

[geokit-rails - 公式Github](https://github.com/geokit/geokit-rails)

