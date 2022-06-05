# new_record?でインスタンスの場合分け

- インスタンスが新規作成されて、情報がないものは`true`  
- インスタンスに既に情報が保存されている場合は`false`

# 具体例

以下のように、インスタンスが新規作成か保存済みかによってボタンの文字列を場合分け。

```ruby
 form_with model: [chatroom, chat], class: 'd-inline-flex', local: false do |f|
  = render 'shared/error_messages', object: chat
  .form-group.form-floating
    = f.text_field :body, id: 'fl-text', placeholder: "メッセージ", class: 'form-control input-chat-body', required: ""
    = f.label :body, for: 'fl-text'
  - if chat.new_record?
    = f.submit '送信', class: 'btn btn-primary btn-raised'
  - else
    = f.submit '更新', class: 'btn btn-primary btn-raised'
```

# 参考

[new_recode? - 公式GitHub](https://github.com/rails/rails/blob/984c3ef2775781d47efa9f541ce570daa2434a80/activerecord/lib/active_record/persistence.rb#L563)

[new_record?で場合分け ❏Rails❏ - qiita](https://qiita.com/ITmanbow/items/3f0be316fedec174d545)
