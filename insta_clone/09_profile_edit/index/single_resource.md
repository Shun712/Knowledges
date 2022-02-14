# 単数形リソースとは？

ただ一つのリソース(resource)に対するCRUD処理を行うためのルーティングを生成する。
リソース(account)は一つだけなので、urlに`:id`が含まれない。  
また、一覧画面(indexアクション)が必要ないので、GETリクエストはリソースの表示(showアクション)である。

```
edit_mypage_account GET    /mypage/account/edit(.:format)   mypage/accounts#edit
mypage_account      PATCH  /mypage/account(.:format)        mypage/accounts#update
                    PUT    /mypage/account(.:format)        mypage/accounts#update
```

# 複数形リソースとは?

複数のリソース(resources)に対する7つのCRUD処理を行うためのルーティングを生成する。
# 単数形リソースとは？

ただ一つのリソース(resource)に対するCRUD処理を行うためのルーティングを生成する。
リソース(account)は一つだけなので、urlに`:id`が含まれない。  
また、一覧画面(indexアクション)が必要ないので、GETリクエストはリソースの表示(showアクション)である。

```
edit_mypage_account GET    /mypage/account/edit(.:format)   mypage/accounts#edit
mypage_account      PATCH  /mypage/account(.:format)        mypage/accounts#update
                    PUT    /mypage/account(.:format)        mypage/accounts#update
```

# 複数形リソースとは?

複数のリソース(resources)に対する7つのCRUD処理を行うためのルーティングを生成する。

# 参考

[Railsガイド - 単数形リソース](https://railsguides.jp/routing.html#%E5%8D%98%E6%95%B0%E5%BD%A2%E3%83%AA%E3%82%BD%E3%83%BC%E3%82%B9)

[resourceとresourcesの違い - qiita](https://qiita.com/ryuuuuuuuuuu/items/e5960c7fecad4ef1301b)
# 参考

[Railsガイド - 単数形リソース](https://railsguides.jp/routing.html#%E5%8D%98%E6%95%B0%E5%BD%A2%E3%83%AA%E3%82%BD%E3%83%BC%E3%82%B9)

[resourceとresourcesの違い - qiita](https://qiita.com/ryuuuuuuuuuu/items/e5960c7fecad4ef1301b)