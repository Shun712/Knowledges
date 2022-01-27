# delete, delete_all, destroy, destroy_allについて

ActiveRecordでよく使う削除系インスタンスメソッドを整理する。

# 前提

```
class Author < ApplicationRecord
  has_many :books, dependent: :destroy
end

class Book < ApplicationRecord
  belongs_to :author
end
```


## destroy
ActiveReordを介して、指定した条件のレコードを削除する。
Modelに`dependet: :destroy`があると、その関連も一緒に削除される。(Authorを削除したら、booksも削除される。)

これがなければ、Authorは削除されても、Booksだけが残ってしまう。

## 補足
`dependet: :destroy`のほかに`dependet: :delet_all`がある（has_one関連の場合、`dependet: :delete`）
この場合、destroyを実行すると、ActiveRecordを介さないで、直接SQLを実行して削除する。

> `:destroy`を設定した場合と`:delete_all`を設定した場合で、destroyを実行してログを見てみるとわかるが、前者はDELETEクエリが関連の数だけ実行されるが、後者だとDELETEクエリ１回だけ実行する。
>
> つまり、後者の方が効率よく関連を削除できるというメリットがあるということ！

> [delete, delete_all, destroy, destroy_allについて - qiita](https://qiita.com/kamelo151515/items/0fa7fb15a1d2c1e44db2#%E8%A3%9C%E8%B6%B3)

## delete

指定した条件のレコードを直接SQLで実行して削除する。

## destroy_all
`Author.find(1).books.destroy_all`
一人のAuthorに関連しているbooksがActiveRecordを介してすべて削除される。（Authorは削除されない）

## delete_all
`Author.find(1).books.delete_all`
一人のAuthorに関連付けられているbooksをすべてActiveRecordを介さないで削除される。
この場合、deleteと同様にbooksの関連付けなどの設定は無視する(deleteコールバックが呼ばれない)。

# 参考
[dependentオプションまとめ[Ruby on Rails] - qiita](https://qiita.com/takayuu276/items/b86ac6b620d2b15c0164)

[delete, delete_all, destroy, destroy_allについて - qiita](https://qiita.com/kamelo151515/items/0fa7fb15a1d2c1e44db2)