# モデル層からバリデーションを切り出して共通のバリデーションルールを定義する

- 電話番号やURL、カナなど複数のモデルで同じバリデーションを定義していることがある。

- 多くのモデルに跨っていると面倒になるので、バリデーションルールを共通化させる

# ActiveModel::EachValidatorとは

- ある１つの属性のバリデーションルールを定義する時に利用する。

- 例えば、電話番号、メールアドレスなどのフォーマットがある。

# 使い方

```ruby
# app/validators/tel_format_validator.rb

class TelFormatValidator < ActiveModel::EachValidator
  def validate_each(record, attribute, value)
    # 電話番号のフォーマットかどうかを確認したいので、空文字は許可
    return if options[:allow_blank] && value.length.zero?

    # 固定電話と携帯番号(ハイフンなし10桁 or 11桁)を許可
    # 「=~」メソッドによるマッチング
    unless value =~ /\A\d{10}$|^\d{11}\z/
      record.errors[attribute] << (options[:message] || '電話番号の形式に誤りがあります')
    end
  end
end
```

`ActiveModel::EachValidator`を継承したクラスでは、`validate_each`というインスタンスメソッドにバリデーションルールを実装し、その引数である`record、attribute、value`にはそれぞれ、対象のオブジェクト、対象の属性、値が入る。

# モデルへの呼び出し

モデルの`validates`メソッドのオプションとして使える

```ruby
# app/models/user.rb

class User < ApplicationRecord
  validates :tel, presence: true, tel_format: true
  validates :tel2, presence: true, tel_format: { message: '電話番号2の形式に誤りがあります' }
end
```

# 参考

[Railsでモデル層からバリデーションを切り出して共通のバリデーションルールを定義する ActiveModel::EachValidator編
](https://tech.mof-mof.co.jp/blog/rails-each-validator/)

[【Rails】バリデーションの共通化(ActiveModel::EachValidator/ActiveModel::Validater)](https://zenn.dev/ddpmntcpbr/articles/26ed8bded2bc5f)