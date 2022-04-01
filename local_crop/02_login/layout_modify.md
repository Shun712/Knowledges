# バリデーションエラー後のレイアウト崩れ対応

[![Image from Gyazo](https://i.gyazo.com/8757d9d2637ac98a14a1ac613d27fbbd.png)](https://gyazo.com/8757d9d2637ac98a14a1ac613d27fbbd)

# 原因

エラー発生後、inputタグ(名前入力フォーム)とtextareaタグ(メッセージ入力フォーム)を囲むように`＜div class="field_with_errors">`が出現している。

```html
<div class="field_with_errors">
  入力フォーム
</div>
```

エラー発生した際、railsは自動でエラーメッセージを含むフィールドを`field_with_errors`クラスを持つdivタグで囲む。
それを利用して、`field_with_errors`を指定してCSSで**エラー発生しているフォームを赤くして目立たせている**。

> Railsでは、エラーメッセージを含むフィールドは自動的にfield_with_errorsクラスを持つdivタグで囲まれます。これを利用して、エラーメッセージをもっと目立たせるようにcssルールを定義しても構いません。
> [Active Record バリデーション - Railsガイド](https://railsguides.jp/active_record_validations.html)

# 解決策

### 1. 自動挿入されないようにする

(config/application.rb)
```ruby
module SampleApp
  class Application &lt; Rails::Application
  # 他省略..
  config.action_view.field_error_proc = Proc.new { |html_tag, instance| html_tag }
  end
end
```
しかし、これではRailsが提供してくれている機能を自ら使えなくしている。

### 2. 追加されたクラスにCSSでスタイルを当てる

```scss
.field_with_errors {
  display: contents;
}
```

# 参考
[Active Record バリデーション - Railsガイド](https://railsguides.jp/active_record_validations.html)

[Railsのエラーメッセージでフォームのレイアウトが崩れる](https://zenn.dev/aosan/scraps/2f65d7dc30fc47)

[Railsのバリデーションエラーで、「field_with_errors」によるレイアウト崩れを防ぐ](https://yukimasablog.com/rails-field-with-errors)