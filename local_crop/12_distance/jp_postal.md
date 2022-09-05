# 住所自動入力

1. viewの設定

```ruby
# app/views/devise/registrations/new.html.erb

form_for...

  <div class="field">
    <%= f.label :postal_code %><br>
    <%= f.text_field :postal_code %>
  </div>

  <div class="field">
    <%= f.label :prefecture_code %><br>
    <%= f.collection_select :prefecture_code, JpPrefecture::Prefecture.all, :name, :name %>
  </div>

  <div class="field">
    <%= f.label :city %><br>
    <%= f.text_field :city %>
  </div>

  <div class="field">
    <%= f.label :street %><br>
    <%= f.text_field :street %>
  </div>
  <div class="field">
    <%= f.label :other_address %><br>
    <%= f.text_field :other_address %>
  </div>
```

2. gemの追加

```ruby
gem 'jp_prefecture' # 都道府県コードから都道府県名を変換するgem
gem 'jquery-rails' # RailsでjQueryを使えるようにするgem
```

3. jquery.jpostal.jsを導入

[![Image from Gyazo](https://i.gyazo.com/767db40a7e7c89459590f00ec8442d34.png)](https://gyazo.com/767db40a7e7c89459590f00ec8442d34)

解凍後、「jquery.jpostal.js」のファイルを見つけ、
このファイルをapp/assets/javascripts 下に格納。

4. application.jsの編集

```ruby
# app/assets/javascripts/application.js

//= require rails-ujs <--削除
//= require jquery <--追加
//= require jquery_ujs <--追加
//= require activestorage
//= require turbolinks
//= require jquery.jpostal <--追加
//= require_tree .

$(function() {
  $(document).on('turbolinks:load', () => {
    $('#user_postal_code').jpostal({
      postcode : [
        '#user_postal_code'
      ],
      address: {
        "#user_prefecture_code": "%3", // # 都道府県が入力される
        "#user_city"           : "%4%5", // # 市区町村と町域が入力される
        "#user_street"         : "%6%7" // # 大口事務所の番地と名称が入力される
      }
    });
  });
});


// # 入力項目フォーマット
// #   %3  都道府県
// #   %4  市区町村
// #   %5  町域
// #   %6  大口事業所の番地 ex)100-6080
// #   %7  大口事業所の名称
```

# うまく動作しないとき

以下をhtmlに直接埋め込む。

```html
# app/views/devise/registrations/new.html.erb

<script type="text/javascript" src="//jpostal-1006.appspot.com/jquery.jpostal.js"></script>
```

# 参考

[jquery.jpostal.js - Github](https://github.com/ninton/jquery.jpostal.js/)

[【jpostal】　jQuery　住所自動入力　rails おそらく一番簡単な方法で - qiita](https://qiita.com/thk__u/items/e5403e717e3ee3c3f64e)

[【Rails】jpostalとjp_prefectureを用いて住所自動入力の実装 - qiita](https://qiita.com/mattan5271/items/278c1d660a225a3eca18)

[【Rails】jpostalとjp_prefectureを用いて住所自動入力の実装 - qiita](https://qiita.com/mattan5271/items/278c1d660a225a3eca18)

[最高の住所入力フォームを作ろう！](https://www.sukerou.com/2020/03/blog-post_26.html)

[【Rails5】Deviseを使って会員登録を行い、郵便番号から住所を自動入力にする方法](https://mimemo.io/m/5dn7jlK2BXor9Ye)

[郵便番号による住所自動入力機能について - qiita](https://qiita.com/ryo___eng/items/e9f59375d75236a98b1d)

[Ruby on Rails】郵便番号から住所を自動入力 - qiita](https://qiita.com/japwork/items/8667a076777fab35c0c4)

[郵便番号から該当する住所を自動で入力できるjQueryプラグイン「jquery.jpostal.js」](https://www.dataplan.jp/blog/jquery/2834)

[Ruby on Rails　住所自動入力実装方法 - qiita](https://qiita.com/tiger26/items/d67582c7439b7f582f35)