# faviconを設定

アプリにfaviconをつけると、ブラウザのタブにアイコンが表示される。

# faviconを作成

icons8 | アイコン無料ダウンロード（https://icons8.jp/icons/set/favicon）

# assets/assets/images配下にfavicon.icoファイルを設置

`assets/assets/images/favicon.ico`

#  faviconを読み込むために、「app/views/layouts/application.html.erb」内に以下を記述

```ruby
<html>
  <head>
<!--(省略) -->

    <%= favicon_link_tag('favicon.ico') %>

<!--(省略) -->
  </head>
```

# サーバー再起動

`$ bundle exec rails s`

# 参考

[Railsでfaviconを設定する手順 - qiita](https://qiita.com/shimataro1988/items/9d131585470c4d9e163c)
