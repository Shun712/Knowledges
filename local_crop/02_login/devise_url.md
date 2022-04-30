# DeviseのURLを変更

仮にdeviseでUserモデルを作成した場合、URLには必ず`/users`という文字列が含まれてしまう。

# 設定方法

```ruby
Rails.application.routes.draw do
  # Deviseのマッピングはするが、skipして何も設定しない
  devise_for :users, skip: %i[sessions registrations passwords],
             controllers: {
               omniauth_callbacks: 'users/omniauth_callbacks',
               confirmations: 'users/confirmations'
             }
  devise_scope :user do
    get 'login', to: 'users/sessions#new', as: :new_user_session
    post 'login', to: 'users/sessions#create', as: :user_session
    delete 'logout', to: 'users/sessions#destroy', as: :destroy_user_session
    get 'signup', to: 'users/registrations#new', as: :new_user_registration
    post 'signup', to: 'users/registrations#create', as: :user_registration
    get 'password', to: 'users/passwords#new', as: :new_user_password
    post 'password', to: 'users/passwords#create', as: :user_password
    get 'password/edit', to: 'users/passwords#edit', as: :edit_user_password
  end
end
```

ルーティング結果
```ruby
             Prefix                Verb                   URI         Pattern                    Controller#Action
   user_line_omniauth_authorize   GET|POST      /users/auth/line(.:format)                   users/omniauth_callbacks#passthru
    user_line_omniauth_callback   GET|POST      /users/auth/line/callback(.:format)          users/omniauth_callbacks#line
user_twitter_omniauth_authorize   GET|POST      /users/auth/twitter(.:format)                users/omniauth_callbacks#passthru
 user_twitter_omniauth_callback   GET|POST      /users/auth/twitter/callback(.:format)       users/omniauth_callbacks#twitter
          new_user_confirmation     GET         /users/confirmation/new(.:format)            users/confirmations#new
              user_confirmation     GET         /users/confirmation(.:format)                users/confirmations#show
                                    POST        /users/confirmation(.:format)                users/confirmations#create
               new_user_session     GET         /login(.:format)                             devise/sessions#new
                   user_session     POST        /login(.:format)                             devise/sessions#create
           destroy_user_session     DELETE      /logout(.:format)                            devise/sessions#destroy
          new_user_registration     GET         /signup(.:format)                            devise/registrations#new
              user_registration     POST        /signup(.:format)                            devise/registrations#create
              new_user_password     GET         /password(.:format)                          devise/passwords#new
                  user_password     POST        /password(.:format)                          devise/passwords#create
             edit_user_password     GET         /password/edit(.:format)                     devise/passwords#edit
                       password     PATCH       /password(.:format)                          devise/passwords#update
           update_user_password     PUT         /password(.:format)                          devise/passwords#update
```

# 参考

[[Rails]Deviseで任意のルーティングだけを行う - qiita](https://qiita.com/chamao/items/de00920c343a3e237d20)

[Rails: deviseのURLをカスタムしたい - qiita](https://qiita.com/suin/items/b479000c49d2468a6260)

[DeviseのURLを変更する](https://note.com/kezzytak/n/n2c8c53f71346)

[【Rails】gem ‘devise’で自動作成されるルーティングを取捨選択する方法](https://techtechmedia.com/routes-devise/)

[[Rails] devise sign_in/sign_outのデフォルトルーティングをカスタマイズしてlogin/logoutにする](https://tech.mof-mof.co.jp/blog/devise-custom-routes/)