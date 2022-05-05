# RSpecでimgタグをテストする

`<img class="crop-detail" src="http://localhost:3000/rails/active_storage/blobs/redirect/eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaHBGQT09IiwiZXhwIjpudWxsLCJwdXIiOiJibG9iX2lkIn19--f16e6e5d85c7f74e7082e9c0074e6e7e02785bd3/test.png">`

HTMLのimgタグからalt属性やsrc属性をチェックスことで意図した内容が表示されているか確認する。

# src属性

画像のファイル名で含まれるか確認する。  
`$`により曖昧検索をしてくれる。

`expect(page).to have_selector("img[src$='test.png']")`

# 参考

[【RSpec】画像の登録と表示についてテストする](https://study-diary.hatenadiary.jp/entry/2020/10/16/133144)

[RSpecでimgタグのオプションをテストする(alt, srcなど) - qiita](https://qiita.com/koki0527/items/26389de0497762527244)