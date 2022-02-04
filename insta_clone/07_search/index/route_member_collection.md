# RESTfulなアクションを追加

デフォルトで作成されるRESTfulなルーティングは7つだが、必要であれば、**追加することも可能**である。

# member

```ruby
resources :photos do
  member do
    get 'preview'
  end
end
```
上の例は、GETリクエストと、`photos/1/preview`を認識し、リクエストをPhotosコントローラーのpreviewアクションにルーティングし、リソースidを`params[:id]`に渡す。  
同時に`preview_photo_path`や`preview_photo_url`ヘルパーも作成される。  

以下の形も同様である。
```ruby
resources :photos do
  get 'preview', on: :member
end
```
ただ、リソースidは**`params[:photo_id]`**となる。

# collection

```ruby
resources :photos do
  collection do
    get 'search'
  end
end
```
上の例は、GETリクエストと、`photos/search`を認識し、リクエストをPhotosコントローラーのsearchアクションにルーティングする。  
同時に`search_photos_path`や`search_photos_url`ヘルパーも作成される。  

# 参考
[Railsガイド - restfulなアクションをさらに追加する](https://railsguides.jp/routing.html#restful%E3%81%AA%E3%82%A2%E3%82%AF%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%92%E3%81%95%E3%82%89%E3%81%AB%E8%BF%BD%E5%8A%A0%E3%81%99%E3%82%8B)