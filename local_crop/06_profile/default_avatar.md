# ActiveStorage/アバター画像をデフォルトで設定

```ruby
# app/models/user.rb

before_create :default_image

def default_image
  if !self.image.attached?
    self.image.attach(io: File.open(Rails.root.join('app', 'assets', 'images', 'event_default.png')), filename: 'default-image.png', content_type: 'image/png')
  end
end
```

ビューファイルにif文を書いていたが、簡略化できる。
```ruby
<% if event.image.attaced? %>
 <%= image_tag event.image %>
<% else %>
 <%= image_tag 'dehault.img' %>
<% end %>

#変更後
<%= image_tag event.image %>
```

# 参考

[Active Storageでデフォルト画像を設定する - qiita](https://qiita.com/mashihiko_397/items/569384b8f8f333b3168e)

[[HowTo]ActiveStorage/アバター画像を登録&表示 - qiita](https://qiita.com/Tatsu88/items/d68cdfa42a08b2713f37)