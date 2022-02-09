# 09 プロフィール編集機能

# やったこと

- 編集画面は/mypage/account/editというパスとする
- アバターとユーザー名を変更できるようにする
- アバター選択時（ファイル選択時）にプレビューを表示する
- 以降の課題でもマイページに諸々追加するのでそれを考慮した設計とする（ルーティングやコントローラやレイアウトファイルなど）

# resource

ただ一つのリソース(resource)に対するCRUD処理を行うためのルーティングを生成する。
リソース(account)は一つだけなので、urlに`:id`が含まれない。  
また、一覧画面(indexアクション)が必要ないので、GETリクエストはリソースの表示(showアクション)である。

```
edit_mypage_account GET    /mypage/account/edit(.:format)   mypage/accounts#edit
mypage_account      PATCH  /mypage/account(.:format)        mypage/accounts#update
                    PUT    /mypage/account(.:format)        mypage/accounts#update
```

> [単数形リソースとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/09_profile_edit/index/single_resource.md)

# cache
バリテーションの失敗後でも、アップロードしたしたファイルを記憶・保持してくれる機能のことである。

[![Image from Gyazo](https://i.gyazo.com/05c40e04e4387a1f96f47463c540fd9d.png)](https://gyazo.com/05c40e04e4387a1f96f47463c540fd9d)

> [cacheとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/09_profile_edit/index/cache.md)

# 学んだこと

- ボッチ演算子を使う場合、レシーバーのオブジェクトが`nil`であってもエラーが起こらずに`nil`を返す。

- `mypage`という名前空間を使うことで、自分のユーザーだけを編集できるようにする（他人がURLで取得して勝手に編集できないようにする）。