# 日付を範囲で取得する

今日: `Time.zone.now.all_day`  
昨日: `1.day.ago.all_day`  
一週間前: `1.day.week.all_day`  
一ヶ月前: `1.day.month.all_day`

```ruby
2.3.4 :001 > Time.zone.now.all_day
 => Sat, 24 Feb 2018 00:00:00 JST +09:00..Sat, 24 Feb 2018 23:59:59 JST +09:00

2.3.4 :002 > 1.day.ago.all_day
 => Fri, 23 Feb 2018 00:00:00 JST +09:00..Fri, 23 Feb 2018 23:59:59 JST +09:00

2.3.4 :003 > 1.week.ago.all_day
 => Sat, 17 Feb 2018 00:00:00 JST +09:00..Sat, 17 Feb 2018 23:59:59 JST +09:00

2.3.4 :004 > 1.month.ago.all_day
 => Wed, 24 Jan 2018 00:00:00 JST +09:00..Wed, 24 Jan 2018 23:59:59 JST +09:00 
```

# beginning_of_dayとかと組み合わせる

```ruby
2.3.4 :007 > 1.week.ago.beginning_of_day
 => Sat, 17 Feb 2018 00:00:00 JST +09:00 

2.3.4 :008 > 1.week.ago.end_of_day
 => Sat, 17 Feb 2018 23:59:59 JST +09:00 
```

`..`で範囲として取得してみる。

```ruby
# 一週間分の範囲を取得する
Book.where(created_at: 1.week.ago.beginning_of_day..Time.zone.now.end_of_day)
```

# 参考

[Rails で1日前とか1週間前とか](https://yatta47.hateblo.jp/entry/2018/02/24/221927)