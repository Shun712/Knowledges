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

# 参考

[Rails link_toでアンカーを設定する - qiita](https://qiita.com/tatsuya1156/items/595fe0df912c6c89f991)