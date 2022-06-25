# 表示中のページのパスを判定する方法

`current_page?`メソッドを用いて、表示中のページのパスを判定できる。

# 具体例

```ruby
# root_path かどうか
current_page?(root_path)

# /users/:id が current_user かどうか
current_page?(current_user)

# 任意のコントローラ/アクションかどうか
current_page?(controller: 'foo', action: 'bar')
```

# 参考

[current_page?](https://apidock.com/rails/ActionView/Helpers/UrlHelper/current_page%3f)

[Railsで表示中のページのパスを判定する方法 - qiita](https://qiita.com/zenizh/items/8b684eefc989d9a56427)