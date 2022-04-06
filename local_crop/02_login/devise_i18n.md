# i18nでdeviseのビューを日本語にする

devise-i18nが効かなかったので備忘録。

# 実装手順

### 1. devise-i18nをインストール

```ruby
# Gemfile
gem 'devise-i18n'
```

### 2. deviseのビューを作成

```ruby
$ rails g devise:i18n:views user
$ rails g devise:i18n:locale ja
```

### 3. config/application.rbでデフォルト言語を設定

```ruby
# config/application.rb
module MessageApp
  class Application < Rails::Application
    config.load_defaults 6.1

    #以下の一文を追加
    config.i18n.default_locale = :ja  #:jaはjapaneseのja

  end
end
```

# 参考

[【Rails】i18nでdeviseのビューを日本語にする](https://ichitasu.com/devise-i18n/)

[Devise Viewをカスタマイズするとdevise-i18nが効かない](https://blog.tanebox.com/archives/590/)