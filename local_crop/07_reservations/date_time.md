# Dateクラス

```ruby
Date.today
#=> Mon, 25 Feb 2022

Date.new(2022,1,2)
#=> Fri, 01 Jan 2022
```

`Date.current`で`application.rb`の設定を参照する「今日」が取得できる。

# Timeクラス

```ruby
Time.current
#=> Mon, 25 Feb 2022 12:03:19 UTC +00:00  # Railsのapplication.rbのconfig.time_zoneをみている

Time.new(2022,1,2,3,4,5)
#=> 2022-01-02 03:04:05 +0900
```

`Time.current`でも今の情報が取れますが`now`とは参照するタイムゾーンが異なる。

# タイムゾーン

> コンピュータの世界では標準をUTC (協定世界時：Coordinated Universal Time)としています。これは日本よりも9時間遅い時刻、つまりUTCからみるとJST (日本標準時：Japan Standard Time) は9時間進んでいると表現することができます。  
> [時刻や日付を扱うメソッドの基本情報まとめ【Ruby】【Rails】](https://fuchiaz.com/ruby-rails-time-date/)

Railsでは、`config/application.rb`に設定を書いておくことでタイムゾーンを設定できる。
```ruby
config.time_zone = 'Tokyo'
config.time_zone = 'Asia/Tokyo'
# どちらでもOK
```

`Time.now` `Date.today` `DateTime.now`は環境変数またはシステムのタイムゾーン設定を、`Time.currentなどのcurrent`は`application.rb`に設定したタイムゾーン設定が利用される。

# 参考

[時刻や日付を扱うメソッドの基本情報まとめ【Ruby】【Rails】](https://fuchiaz.com/ruby-rails-time-date/)

[■一時間後の時刻を表示する](http://www.openspc2.org/reibun/Ruby/time/007/index.html)