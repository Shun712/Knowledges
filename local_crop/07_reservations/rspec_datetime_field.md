# 日時フォームのシステムスペック

```ruby
fill_in "task[deadline]", with: "2022-5-5-15:00T00:16:12"
expect(page).to have_content "2022-5-5-15:00T00:16:12"
```

これでテストを実行すると、
`202255-15:00T00:16:12`と入力されてしまっている。

# 解決方法

年の部分が6桁分入るため、頭を`00`で埋めることでずれ込まないようにする。  
`fill_in "task[deadline]", with: "002022-5-5-15:00T00:16:12"`

# 参考

[SystemSpecでのdate_fieldへの入力方法 - teratail](https://teratail.com/questions/301872)

[rspec date_field の値のテストが出来ない - qiita](https://qiita.com/TatsuyaIsamu/items/09018d155733060c7a08)