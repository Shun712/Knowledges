# link_toでアンカーを設定

チャットルームで最新のコメントに遷移させるため、アンカーを設定する

# ビューを設定

フッターに`id`を設定

```ruby
footer.bg-accent.pt-2.sort id="bottom"
  .my-sm-0.text-center.pt-1.flex-column
    .d-inline-flex.align-items-center.text-nowrap.fs-sm
      .ps-sm-2.text-muted
        span.fw-medium.text-light.me-1
          = link_to '使い方', about_path
      .ps-sm-1.ps-1.border-start.border-light
        span.fw-medium.text-light.me-1
          = link_to '利用規約', terms_path
      .ps-sm-1.ps-1.border-start.border-light
        span.fw-medium.text-light.me-1
          = link_to 'プライバシーポリシー', privacy_path
      .ps-sm-1.ps-1.border-start.border-light
        span.fw-medium.text-light.me-1
          = link_to 'お問い合わせ', new_feedback_path
  .pb-4.fs-xs.text-center.text-md-center.text-white
    | © LocalCrops. All rights reserved.
```

# link_toにanchorを指定する

```ruby

.table-responsive.my-chats
  table.table
    tr
      td width="25%"
        = image_tag current_user.partner(chatroom).avatar, class: 'rounded-circle me-1', size: '30x30'
        br
          = link_to current_user.partner(chatroom).username.truncate(6), user_path(current_user.partner(chatroom))
      td valign="middle"
        = link_to chatroom.decorate.chat_text, chatroom_path(chatroom, anchor: 'bottom')
      td width="120px" valign="middle"
        = chatroom.decorate.created_at
```

# 参考

[Rails link_toでアンカーを設定する - qiita](https://qiita.com/tatsuya1156/items/595fe0df912c6c89f991)