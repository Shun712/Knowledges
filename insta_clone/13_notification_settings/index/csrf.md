# Formの隠し要素

Railsではフォームを作ると、文字エンコードとauthenticity_tokenが自動で含まれる。  
authenticity_tokenはCSRF対策のため、GETメソッド以外でトークンが作成される。

Railsサーバーに対して、トークン抜きでリクエストを送っても原則拒否される。
```ruby
<%= form_tag do %>
  Form contents
<% end %>
```

```ruby
<form accept-charset="UTF-8" action="/home/index" method="post">
  <div style="margin:0;padding:0">
    <input name="utf8" type="hidden" value="&#x2713;" />
    <input name="authenticity_token" type="hidden" value="f755bb0ed134b76c432144748a6d4b7a7ddf2b71" />
  </div>
  Form contents
</form>
```

# CSRFとは?

> CSRF（クロスサイトリクエストフォージェリ）攻撃は、認証が完了したとユーザーが信じているWebアプリケーションのページに、悪意のあるコードやリンクを仕込むというものです。  
> [クロスサイトリクエストフォージェリ（CSRF）- Railsガイド](https://railsguides.jp/security.html#%E3%82%AF%E3%83%AD%E3%82%B9%E3%82%B5%E3%82%A4%E3%83%88%E3%83%AA%E3%82%AF%E3%82%A8%E3%82%B9%E3%83%88%E3%83%95%E3%82%A9%E3%83%BC%E3%82%B8%E3%82%A7%E3%83%AA%EF%BC%88csrf%EF%BC%89)

フォージェリとは偽物のことであり、悪意のあるユーザーがその人の意志とは関係なく
JavaScriptなどでコードを仕込んで、サーバー側にリクエストを送ってしまうこと。

# CSRF対策

tokenはサーバー側から毎回ランダムに生成され、リクエスト時にこのトークンがサーバー側と一致するか検証される。  
これはフォームに対する送信を確認するもので、Railsから送ったフォーム以外からの送信を排除するための仕掛けとなっている。

# 参考

[Action View フォームヘルパー - Railガイド](https://railsguides.jp/form_helpers.html)

[クロスサイトリクエストフォージェリ（CSRF）- Railsガイド](https://railsguides.jp/security.html#%E3%82%AF%E3%83%AD%E3%82%B9%E3%82%B5%E3%82%A4%E3%83%88%E3%83%AA%E3%82%AF%E3%82%A8%E3%82%B9%E3%83%88%E3%83%95%E3%82%A9%E3%83%BC%E3%82%B8%E3%82%A7%E3%83%AA%EF%BC%88csrf%EF%BC%89)

[【第１回】 Railsガイドの「Action View フォームヘルパー」をひたすらまとめていく 【Formの概要編】](https://tech-essentials.work/course_outputs/201)

[Rails – formヘルパーとCSRF対策](http://taustation.com/rails-form-helper-csrf-countermeasure/)