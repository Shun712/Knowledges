# 小数点の桁数指定

round関数を使う場合  
数値(Integer or Float)を四捨五入して返す


```ruby
1.2345.round    #=> 1
1.2345.round(1) #=> 1.2
1.2345.round(2) #=> 1.23
1.2345.round(3) #=> 1.235 (四捨五入)
puts 1.2345.round(3) #=> 1.235
```

# 参考

[Rubyで小数点桁数指定 - qiita](https://qiita.com/seteen/items/c8ac3a6349cd53ef25b7)