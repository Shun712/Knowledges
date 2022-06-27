# ransackでソート機能を実装

ソート機能を実装することでレコードを昇順、降順に並び替えできる。

# ビューファイル

```ruby
<%= sort_link(@q, :データベースのカラム名, "表示される文字" %>

<%= sort_link(@q, :age, "年齢" %>
```

# コントローラ

```ruby
def index
  @users = @q.result
end
```

これだけで、ソート機能が実装できる。

# 参考

[ransack - 公式GitHub](https://github.com/activerecord-hackery/ransack)

[【Rails】 ransackを使って検索機能がついたアプリを作ろう！ - pikawaka](https://pikawaka.com/rails/ransack#%E3%82%BD%E3%83%BC%E3%83%88%E6%A9%9F%E8%83%BD%E3%82%92%E5%AE%9F%E8%A3%85%E3%81%97%E3%82%88%E3%81%86)