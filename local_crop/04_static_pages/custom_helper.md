# カスタムヘルパーを理解する

元からあるメソッドでカバーしきれないものを自作で補うことを**ヘルパー/カスタムヘルパー**と呼ぶ。

# 定義場所

例えば、`app/helpers/application_helper.rb`に必要な機能を書き込んでいくことで、`app/views/layouts/application.html.erb`の`ビュー`に影響を与える。

# 使い方

```ruby
# application/helper.eb

module ApplicationHelper

  def full_title(page_title)
    base_title = "Ruby"
    if page_title.empty?
      base_title
    else
      "#{base_title} | #{page_title}"
    end
  end

end
```

```ruby
# application.html.erb

<!DOCTYPE html>
          <html>
          <head>
          <title><%= full_title(yield(:title)) %></title>
  〜中略〜
</head>
<body>

  〜後略〜

</body>
</html>
```

このようにすることで、`application.html.erb`側に書かれている`title`タグに
`full_title(page_title)`メソッドの効果が反映される。

`コントローラやモデルにカスタムヘルパーを反映させたい場合、別の設定が必要になる。`

# 参考

[ヘルパー(カスタムヘルパー)ってなんぞ？ - qiita](https://qiita.com/sanstktkrsyhsk/items/67e9d88b939ccdcf46e8)

[【Rails入門】helperの使い方まとめ](https://www.sejuku.net/blog/28563)