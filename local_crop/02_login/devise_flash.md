# deviseを用いたフラッシュメッセージ表示方法

ログインした際のフラッシュメッセージは**CSSで自分でカスタマイズできる**。

# 実装手順

### 1. `app/views/layouts/application.html.slim`に表示領域を確保

(app/views/layouts/application.html.slim)
```ruby
= render 'shared/flash_messages'
```

(app/views/shared/_flash_messages.html.slim)

```ruby
- flash.each do |message_type, message|
  p class=("flash #{message_type}") = message
```

### 2. CSSをカスタマイズ

```scss
.alert {
  position: relative;
  padding: 0.75rem 1.125rem;
  margin-bottom: 1rem;
  border: 1px solid transparent;
  border-radius: 0.4375rem;
  color: #e5955f;
  background-color: #fff6f0;
  border-color: #ffe0cb;
}
```

# 参考

[【Rails基礎】deviseを用いたフラッシュメッセージを表示する方法を簡単に解説](https://techtechmedia.com/flash-messages-rails/)