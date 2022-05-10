# bootstrap5を使用したkaminariを実装

前提としてbootstrap5がインストールされていること。

```ruby
gem 'kaminari'
gem 'bootstrap5-kaminari-views'
```

```ruby
<ul class="users">
  <% @users.each do |user| %>
    <li>
      <%= gravatar_for user, size: 50  %>
      <%= link_to user.name, user, class: "user" %>
    </li>
  <% end %>
</ul>

<%= paginate @users, theme: 'bootstrap-5' %>　　#ここがページネーション
```

`theme: 'bootstrap-5'`
これをつけることでCSSが適用される。

# デザイン変更

```scss
/*ページネーション自体のデザイン*/
.pagination>li>a {          
  border: none;     /*枠線をなくす*/
  color: #696969;   /*文字の色を変える*/
}

/* 表示しているページ番号のデザイン */
.pagination>.active>a {     
  background: #93c9ff;     /*背景の色を変える*/
  border-radius: 15px;     /*角を丸くする*/
}

/*ホバー時のデザイン*/
.pagination>li>a:hover {        
  border-radius: 15px;    /*角を丸くする*/
}
```

[![Image from Gyazo](https://i.gyazo.com/529e5a2bc9db93bee752ccbfcf64bf4c.png)](https://gyazo.com/529e5a2bc9db93bee752ccbfcf64bf4c)

# ラベルを変更する

FontAwesomeを実装すればよりシンプルなデザインになる。

```yaml
ja:
  views:
    pagination:
      first: <i class="fas fa-angle-double-left"></i>
      last: <i class="fas fa-angle-double-right"></i>
      previous: <i class="fas fa-angle-left"></i>
      next: <i class="fas fa-angle-right"></i>
      truncate: "..."
```

[![Image from Gyazo](https://i.gyazo.com/9e73f24aa216baf3ee0018ed74cc2930.png)](https://gyazo.com/9e73f24aa216baf3ee0018ed74cc2930)

# 参考

[kaminariを使用してbootstrap5でCSSを追加する - qiita](https://qiita.com/mocomou_/items/c3cce91c241e08f9a50b)

[【Rails初心者】ページネーションを実装して自分好みにデザインを変える - qiita](https://qiita.com/rio_threehouse/items/313824b90a31268b0074)
