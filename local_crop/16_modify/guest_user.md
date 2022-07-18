# ゲストユーザーを作成

ゲストログイン機能が無いと、新規登録が面倒という理由でポートフォリオを見てすらもらえない可能性が高くなる。ポートフォリオを閲覧してもらうに当たり離脱を防ぐためにゲストログインを実装した。

# 実装

```ruby
# config/routes.rb

  devise_scope :user do
    post 'guest_login', to: 'users/sessions#guest_login', as: :guest_session
  end
```

```ruby
# app/controllers/users/sessions_controller.rb

def guest_login
  user = User.guest
  sign_in user
  redirect_to crops_path, success: 'ゲストユーザーとしてログインしました'
end
```

```ruby
# app/models/user.rb

def self.guest
  find_or_create_by!(email: 'guestuser@example.com')
  end
```

```ruby
# app/views/static_pages/top.html.slim

- unless user_signed_in?
  = link_to 'ゲストログイン（閲覧用）', guest_session_path, method: :post
```

# ゲストユーザーを削除できないようにする

```ruby
# config/routes.rb

  devise_for :users, controllers: {
    registrations: 'users/registrations'
  }
```

```ruby
# app/controllers/users/registrations_controller.rb

class Users::RegistrationsController < Devise::RegistrationsController
  before_action :ensure_normal_user, only: :destroy

  def ensure_normal_user
    if resource.email == 'guest@example.com'
      redirect_to root_path, alert: 'ゲストユーザーは削除できません。'
    end
  end

end
```

# パスワードを変更できないようにする

```ruby
# app/controllers/users/registrations_controller.rb

- before_action :ensure_normal_user, only: :destroy
+ before_action :ensure_normal_user, only: %i[update destroy]
```

```ruby
# config/routes.rb

#   devise_for :users, controllers: {
#     registrations: 'users/registrations'
#   }
# を次に置き換える。（,の付け忘れに注意！）
  devise_for :users, controllers: {
    registrations: 'users/registrations',
    passwords: 'users/passwords'
  }
```

```ruby
# app/controllers/users/passwords_controller.rb

class Users::PasswordsController < Devise::PasswordsController
  before_action :ensure_normal_user, only: :create

  def ensure_normal_user
    if params[:user][:email].downcase == 'guest@example.com'
      redirect_to new_user_session_path, alert: 'ゲストユーザーのパスワード再設定はできません。'
    end
  end
end
```

# 参考

[簡単ログイン・ゲストログイン機能の実装方法（ポートフォリオ用） - qiita](https://qiita.com/take18k_tech/items/35f9b5883f5be4c6e104)

[ゲストログイン機能 [Rails/LexicallyScopedActionFilter:] - qiita](https://qiita.com/orizin/items/ca91fd637bc02a4427aa)