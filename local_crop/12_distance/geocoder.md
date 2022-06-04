# geocoderの設定

### APIキーの取得

[Google Maps Platform](https://mapsplatform.google.com/) からAPIキーを取得する。

APIキーは`.env`で環境変数として管理する。

[【Rails6 / Google Map API】初学者向け！Ruby on Railsで簡単にGoogle Map APIの導入する - qiita](https://qiita.com/nagase_toya/items/e49977efb686ed05eadb)

[Rails5でGoogleMapを表示してみるまで - qiita](https://qiita.com/tiara/items/4a1c98418917a0e74cbb)

### geocoder.rbの設定

```ruby
Geocoder.configure(
  # Geocoding options
  # timeout: 3,                 # geocoding service timeout (secs)
  lookup: :google,         # name of geocoding service (symbol)
  # ip_lookup: :ipinfo_io,      # name of IP address geocoding service (symbol)
  # language: :en,              # ISO-639 language code
  use_https: true,           # use HTTPS for lookup requests? (if supported)
  # http_proxy: nil,            # HTTP proxy server (user:pass@host:port)
  # https_proxy: nil,           # HTTPS proxy server (user:pass@host:port)
  api_key: ENV['GOOGLE_MAP_API_KEY'],               # API key for geocoding service
  # cache: nil,                 # cache object (must respond to #[], #[]=, and #del)

  # Exceptions that should not be rescued by default
  # (if you want to implement custom error handling);
  # supports SocketError and Timeout::Error
  # always_raise: [],

  # Calculation options
  # units: :mi,                 # :km for kilometers or :mi for miles
  # distances: :linear          # :spherical or :linear

  # Cache configuration
  # cache_options: {
  #   expiration: 2.days,
  #   prefix: 'geocoder:'
  # }
)
```

### DBにカラムの追加

`$ rails g migration AddAddressToUser`

```ruby
class AddAddressToUser < ActiveRecord::Migration[6.1]
  def change
    add_column :users, :address, :string
    add_column :users, :latitude, :float
    add_column :users, :longitude, :float
  end
end
 
```

### Gemの追加

`gem 'geocoder'`

### モデルの編集

```ruby
# app/models/user.rb
 geocoded_by :address
 after_validation :geocode, if: :address_changed?
```
`geocoded_by :address` の記述で、addressの文字列から自動で緯度と経度のカラムに値を代入してくれる。  
`after_validation :geocode, if: :address_changed?` の記述で、addressカラムが値が代入される時（createとupdate）に、緯度と経度を住所から変換してくれる。

### コントローラの編集(deviseを使用)

```ruby
# app/controllers/application_controller.rb

def configure_permitted_parameters
    # user登録でユーザー名を登録できるようにする
    devise_parameter_sanitizer.permit(:sign_up, keys: [:username])
    # user更新でユーザー名、メールアドレス、アバター画像を更新できるようにする
    devise_parameter_sanitizer.permit(:account_update, keys: %i[username email avatar address latitude longitude])
  end
```

### ビューの編集

```ruby
<%= form_with(model: @user) do |f| %>
 <div class="field my-3">
   <%= f.label :title %>
   <%= f.text_field :title %>
 </div>
 <div class="field my-3">
   <%= f.label :content %>
   <%= f.text_area :content %>
 </div>
 <div class="field my-3">
   <%= f.label :address %>
   <%= f.text_field :address %>
 </div>
 <div class="actions">
   <%= f.submit %>
 </div>
<% end %>
```

# 動作確認

```ruby
[1] pry(main)> Geocoder.coordinates("東京都渋谷区道玄坂1-12-5渋谷マークシティ")
=> [35.658046, 139.6980562]
```

上記のように座標が返ってきたらOKである。

# 参考

[geocoder - 公式Github](https://github.com/alexreisner/geocoder)

[railsでGoogle Mapの表示の仕方](https://note.com/mosanei/n/n460548e2a62b)

[Google Mapを利用する 【Rails6】【Geocoder】【heroku】 - qiita](https://qiita.com/MandoNarin/items/aa91ffae373a8cfc85d2?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items)

[Rails5 で geocoder を使って、緯度経度の取得する（Google API の設定） - qiita](https://qiita.com/creativival/items/1024719726694f620ad0)