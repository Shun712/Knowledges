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

