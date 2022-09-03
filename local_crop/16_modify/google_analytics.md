# アプリにGoogleAnalyticsを導入

Googleアナリティクスとは、Googleが無料で提供するアクセス解析ツールのことである。

# Googleアナリティクスの登録手順

1. Googleアナリティクス　アカウント登録

[![Image from Gyazo](https://i.gyazo.com/b44ebdbaffc503302a763378c722db07.png)](https://gyazo.com/b44ebdbaffc503302a763378c722db07)

2. 測定対象の指定

[![Image from Gyazo](https://i.gyazo.com/fc0fcd68a12e3902cc517a4d91730c29.png)](https://gyazo.com/fc0fcd68a12e3902cc517a4d91730c29)

[![Image from Gyazo](https://i.gyazo.com/5db54b671938a47f1909eef94fbbc429.png)](https://gyazo.com/5db54b671938a47f1909eef94fbbc429)

[ユニバーサルアナリティクスプロパティの作成]をチェックし、ウェブサイトのURLを登録する。

3. プロパティの登録

[![Image from Gyazo](https://i.gyazo.com/d44cbe1c6acef701d53a443f495e795c.png)](https://gyazo.com/d44cbe1c6acef701d53a443f495e795c)

利用規約に同意するとGoogleアナリティクスの登録が完了する。

# Railsに導入

Googleアナリティクス用の部分テンプレートを用意し、headタグで読み込む。

```ruby
# app/views/shared/_google_analytics.html.slim

script async="" src="https://www.googletagmanager.com/gtag/js?id=G-39E58NFJ90"
javascript:
    window.dataLayer = window.dataLayer || [];

    function gtag() {
        dataLayer.push(arguments);
    }

    gtag('js', new Date());
    gtag("config", "トラッキングID");
    if (#{raw current_user.to_json}) {
        gtag('set', {'user_id': #{raw current_user.to_json}.id});
    }
```

```ruby
# app/views/layouts/application.html.slim

doctype html
html
  head
    meta[name="viewport" content="width=device-width,initial-scale=1"]
    = display_meta_tags(default_meta_tags)
    = csrf_meta_tags
    = csp_meta_tag
    = stylesheet_pack_tag 'application', media: 'all'
    = javascript_pack_tag 'application'
    script src="//jpostal-1006.appspot.com/jquery.jpostal.js" type="text/javascript"
    = favicon_link_tag('favicon.ico')
    - if Rails.env.production?
      = render 'shared/google_analytics'
```

ポイントとなるのが、最後のif文で、ログインしている場合は、`current_user`をjsonに変換してデータを渡してあげている。
また、エスケープ処理を回避させるために`ActionView::Helpers::OutputSafetyHelper`のrawメソッドを使っています。`html_safe`でも同じことができますが、nilだった場合に例外が発生してしまうのでrawメソッドが推奨されている。(Railsガイドより)

# 参考

[Googleアナリティクスの登録・設定方法【2021年版】](https://blog.siteanatomy.com/register-google-analytics/)

[【Rails】Googleアナリティクスを導入する方法【簡単】 - qiita](https://qiita.com/Kiyo_Karl2/items/1bd9012ac6e27b914175)

[RailsでGoogleAnalyticsを設定する - qiita](https://qiita.com/t1gert1ger/items/b9a197e2d85050b9d7d6)