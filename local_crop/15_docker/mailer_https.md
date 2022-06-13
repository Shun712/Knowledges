# アクティベーションURLのhttps設定

`config/environments/production.rb`を以下のように追記する。

```ruby
 config.active_record.dump_schema_after_migration = false
 config.action_mailer.default_url_options = { protocol: 'https', host: "#{ENV['HOST']}/" } # 追記
 config.action_mailer.raise_delivery_errors = true
 config.action_mailer.delivery_method = :smtp
 config.action_mailer.smtp_settings = {
   address: 'smtp.gmail.com',
   port: 587,
   user_name: ENV['GMAIL_ADDRESS'],
   password: ENV['GMAIL_PASSWORD'],
   authentication: :plain,
   enable_starttls_auto: true
}
```

# 参考

[devise confirmation_url in HTTPS - stack overflow](https://stackoverflow.com/questions/21828080/devise-confirmation-url-in-https)