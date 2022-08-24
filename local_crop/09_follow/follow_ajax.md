# Ajaxを用いた非同期フォロー機能の実装

1. フォロワー数にidを付与

```ruby
# app/views/users/show.html.slim

.mb-2.ms-sm-3.me-2.text-muted.align-items-sm-end
  span.fw-medium.text-light.me-1
    div id="follower_count_#{@user.id}"
      = @user.followers.count
  span.text-white.opacity-70 followers
.mb-2.ps-sm-2.ps-2.border-start.border-light.text-muted
  span.fw-medium.text-light.me-1
    div id="following_count_#{@user.id}"
      = @user.following.count
  span.text-white.opacity-70 following
```

2. JavaScriptファイルを作成

```html
# app/views/relationships/create.js.slim

| $('#follow-area-#{@user.id}').html("#{j render('users/unfollow', user: @user)}");
| $("#follower_count_#{@user.id}").html(' #{@user.followers.count} ');
| $("#following_count_#{@user.id}").html(' #{@user.following.count} ');
```

```html
# app/views/relationships/destroy.js.slim

| $('#follow-area-#{@user.id}').html("#{j render('users/follow', user: @user)}");
| $("#follower_count_#{@user.id}").html(' #{@user.followers.count} ');
| $("#following_count_#{@user.id}").html(' #{@user.following.count} ');
```

# 参考

[Ajaxを用いた非同期フォロー機能の実装 - qiita](https://qiita.com/ttf1998seiya/items/337da8a5be455469ec46)

[【Rails】Ajaxを用いた非同期フォロー機能の実装 - qiita](https://qiita.com/mattan5271/items/3a70689b42dd98b4d99b)