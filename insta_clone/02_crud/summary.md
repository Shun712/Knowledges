# 02 投稿のCRUD機能を実装

## fakerとは?

ダミーデータを作成する際に、ある項目のデータを自動で出力してくれるgemである。

> [fakerとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/02_crud/index/faker.md)

## CarrierWaveとは?
ファイルのアップロード機能を簡単に追加する事が出来るgemである。
CarrierWaveは、アップロードしたファイルの保存先はデフォルトで`public/uploads`だが、外部ストレージ(Amazon S3)にも設定できる。

> [CarrierWaveとは？](https://github.com/Shun712/Knowledges/blob/master/insta_clone/02_crud/index/carrierwave.md)

## Swiperとは?
SwiperはJavaScriptライブラリで、JQueryに依存せずJavaScript単体で動作させることができ、CSSとJSを適用することで、画像などをスライドできる機能。

> [swiperとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/02_crud/index/swiper.md)

## 学んだこと

- `rails db:seed`を実行した際に、`NoMethodError: undefined method `posts' for #<User:0x00007f944715e400>`というエラーが発生したのですぐエラー分をググらずに考察してみた。`
`user.posts.create`でエラーが発生したので「関連」が定義できていないと推測したら、案の定`model/user.rb`に`has_many :posts, dependent: :destroy`が記入されていなかった。

- swiperを導入したが、バージョンの違いでうまく表示できていなかった。(`.swiper-container`の廃止の為)
バージョンの確認は必要である。

- `JSON::ParserError: 416: unexpected token at #<file:/Users/shun/insta_rails/db/fixtures/dummy.png>`というエラーが発生したが、解決方法を探してみたがわからず、`rails db:migrate:reset`でエラーが解消した。