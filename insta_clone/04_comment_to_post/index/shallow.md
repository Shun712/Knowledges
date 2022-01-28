# shallowのルーティング

```
resources :posts do
  resources :comments, shallow: true
end
```
以下のような`comments`のルーティングが生成される。

[![Image from Gyazo](https://i.gyazo.com/1765902009fa4e0f0af3484cb70f085c.png)](https://gyazo.com/1765902009fa4e0f0af3484cb70f085c)


>コレクション (index/new/createのような、idを持たないアクション) だけを親のスコープの下で生成するという手法があります。
>
>このとき、メンバー (show/edit/update/destroyのような、idを必要とするアクション)をネストに含めないのがポイントです。
>
> [Rails のルーティング - Railsガイド](https://railsguides.jp/routing.html#%E6%B5%85%E3%81%84%E3%83%8D%E3%82%B9%E3%83%88)

`shallow`は、ネストしたルーティングにおいて、下層にあるテーブルのIDが一意なら、その上にあるテーブルのIDは不要というメリットである。

つまり、`index`、`new`、`create`アクションについては、どのpostのidに紐づくか示さないと一意に保つことができない。

一方、`edit`、`update`、`destroy`アクションについては、postのidがなくても、commentのidでどのコメントか明らかになる。

# 参考

[Railsの”shallow（浅い）”ルーティングを理解する - qiita](https://qiita.com/tanutanu/items/a245f7691c77b56d4cd3)

[Rails のルーティング - Railsガイド](https://railsguides.jp/routing.html#%E6%B5%85%E3%81%84%E3%83%8D%E3%82%B9%E3%83%88)