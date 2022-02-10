# lメソッドとは?

```azure
Tue, 30 Jul 2020 00:12:12 +0000
```

日本人には見慣れない、時刻表示を見慣れた表示にする。

```azure
2020/02/10 09:12:12
```

# 実装手順

(config/application.rb)
```ruby
module TimeFormatSandbox
  class Application < Rails::Application
    # ...

    # デフォルトのロケールを日本（ja）に設定
    config.i18n.default_locale = :ja
  end
end
```

(config/locales/ja.yml)
```yaml  
  time:
    formats:
      default: "%Y年%m月%d日(%a) %H時%M分%S秒 %z"
      long: "%Y/%m/%d %H:%M"
      short: "%m/%d %H:%M"
```

formatsオプションを付けると、書式を切り替えることができる。

```ruby
<td><%= l user.created_at, format: :short %></td>
```

# 参考

[【初心者向け・動画付き】Railsで日時をフォーマットするときはstrftimeよりも、lメソッドを使おう - qiita](https://qiita.com/jnchito/items/831654253fb8a958ec25)

[【Rails】日時フォーマット（lメソッド）](https://boku-boc.hatenablog.com/entry/2020/12/02/224203)