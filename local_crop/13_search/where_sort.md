# rails のwhere句の結果を指定の順番で取り出す方法

idsはArrayで中にCropモデルの取り出したいidが先頭から順番に入っている。

```ruby
crop_ids = [23, 12, 34, 45, 9]
```

しかし、順番が意図している順序にならない。(id順になってしまう)

```ruby
> p = Crop.where(id: ids)
> p
=> [#<crop id: 9, name: 'test_9'>,
#<crop id: 12, name: 'test_12'>,
#<crop id: 23, name: 'test_23'>,
#<crop id: 34, name: 'test_34'>,
```

# order_as_specified gemを使うと意図した順番で取得できる

```ruby
class Crop < ApplicationRecord
  belongs_to :user
  # 追記
  extend OrderAsSpecified
```

```ruby
@crops = Crop.where(id: crop_ids)
             .order_as_specified(id: crop_ids)
```

# おまけ

rails7には、`in_order_of` が用意されている。

# 参考

[order_as_specified
 - 公式GitHub](https://github.com/panorama-ed/order_as_specified)

[Ruby on Railsのwhereで値を順序どおりに取得する方法](https://programming-beginner-zeroichi.jp/articles/139)

[rails のwhere句の結果を指定の順番で取り出す方法は？ - stackoverflow](https://ja.stackoverflow.com/questions/11972/rails-%e3%81%aewhere%e5%8f%a5%e3%81%ae%e7%b5%90%e6%9e%9c%e3%82%92%e6%8c%87%e5%ae%9a%e3%81%ae%e9%a0%86%e7%95%aa%e3%81%a7%e5%8f%96%e3%82%8a%e5%87%ba%e3%81%99%e6%96%b9%e6%b3%95%e3%81%af)