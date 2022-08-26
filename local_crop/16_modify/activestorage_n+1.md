# Active StorageのN+1問題

Active Storageには`with_attached_attachment_name`というスコープが存在する。
`with_attached_attachment_name`内では`includes("#{name}_attachment": :blob)`のように関連付けられたblobをincludeしている。


# モデルのオプション

`has_one_attached`メソッドを使って`with_attached_book_image`というスコープが作成される。

```ruby
class Book < ApplicationRecord
  has_one_attached :book_image
end
```

# with_attached_book_imageでBookを全件取得

```ruby
class BooksController < ApplicationController
  def index
    @books = Book.with_attached_book_image
  end
```

これで、N+1問題が解決します。

#　参考

[Active StorageのN+1問題に対処する](https://shuttodev.hatenablog.com/entry/2019/09/10/012916)

[Active StorageのN+1問題を解決する - qiita](https://qiita.com/ozin/items/f4aea5b244a6aa03caee)