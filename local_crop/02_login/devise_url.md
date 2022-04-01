# DeviseのURLを変更

仮にdeviseでUserモデルを作成した場合、URLには必ず`/users`という文字列が含まれてしまう。

# 設定方法

```ruby
Rails.application.routes.draw do
  # Deviseのマッピングはするが、skipして何も設定しない
  devise_for :users, skip: :all
  devise_scope :user do
    get 'login', to: 'devise/sessions#new', as: :new_user_session
    post 'login', to: 'devise/sessions#create', as: :user_session
    delete 'logout', to: 'devise/sessions#destroy', as: :destroy_user_session
    get 'signup', to: 'devise/registrations#new', as: :new_user_registration
    post 'signup', to: 'devise/registrations#create', as: :user_registration
    get 'password', to: 'devise/passwords#new', as: :new_user_password
    post 'password', to: 'devise/passwords#create', as: :user_password
    get 'password/edit', to: 'devise/passwords#edit', as: :edit_user_password
    patch 'password', to: 'devise/passwords#update'
    put 'password', to: 'devise/passwords#update', as: :update_user_password
    get 'confirmation/new', to: 'devise/confirmations#new', as: :new_user_confirmation
    get 'confirmation', to: 'devise/confirmations#show'
    post 'confirmation', to: 'devise/confirmations#create', as: :user_confirmation
  end
end
```

ルーティング結果
```ruby
                           Prefix Verb       URI         Pattern                    Controller#Action
                        new_user_session     GET    /login(.:format)             devise/sessions#new
                            user_session     POST   /login(.:format)             devise/sessions#create
                    destroy_user_session     DELETE /logout(.:format)            devise/sessions#destroy
                   new_user_registration     GET    /signup(.:format)            devise/registrations#new
                       user_registration     POST   /signup(.:format)            devise/registrations#create
                       new_user_password     GET    /password(.:format)          devise/passwords#new
                           user_password     POST   /password(.:format)          devise/passwords#create
                      edit_user_password     GET    /password/edit(.:format)     devise/passwords#edit
                                password     PATCH  /password(.:format)          devise/passwords#update
                    update_user_password     PUT    /password(.:format)          devise/passwords#update
                   new_user_confirmation     GET    /confirmation/new(.:format)  devise/confirmations#new
                            confirmation     GET    /confirmation(.:format)      devise/confirmations#show
                       user_confirmation     POST   /confirmation(.:format)      devise/confirmations#create
```

# 参考

[[Rails]Deviseで任意のルーティングだけを行う - qiita](https://qiita.com/chamao/items/de00920c343a3e237d20)

[Rails: deviseのURLをカスタムしたい - qiita](https://qiita.com/suin/items/b479000c49d2468a6260)

[DeviseのURLを変更する](https://note.com/kezzytak/n/n2c8c53f71346)