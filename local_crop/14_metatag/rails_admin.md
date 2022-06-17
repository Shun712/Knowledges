# rails_adminの導入

簡易的な管理者側機能を実装できる。

# deviseの導入

`gem 'devise'`

# rails_adminの導入

`gem 'rails_admin', '~> 2.0'`

# cancancanの導入

`gem 'cancancan'`

これでgemの導入は完了。

# 管理者権限の設定

`$ rails g cancan:ability`

これによって生成されたモデルを編集し、管理者権限を持つユーザに管理画面へのアクセスと全てのモデルに対しての全ての操作（新規保存、編集、削除など）」を許可する設定をする。

```ruby
# app/models/ability.rb

class Ability
  include CanCan::Ability

  def initialize(user)
    if user&.admin?
      can :access, :rails_admin
      can :manage, :all
    end
  end
end
```

# config/initializers/rails_admin.rbも以下のように変更

```ruby
# config/initializers/rails_admin.rb

RailsAdmin.config do |config|

  ### Popular gems integration

  ## == Devise ==
  config.authenticate_with do
    warden.authenticate! scope: :user
  end
  config.current_user_method(&:current_user)

  # == CancanCan ==
  config.authorize_with :cancancan


  config.actions do
    dashboard                     # mandatory
    index                         # mandatory
    new
    export
    bulk_delete
    show
    edit
    delete
    show_in_app
  end
end
```

# 管理者権限の付与

ユーザが管理者がどうかを判断する為に、「admin」カラムを追加し、ture or falseで判断

`$ rails g migration add_column_to_users`

```ruby
class AddColumnToUsers < ActiveRecord::Migration[6.1]
  def change
    add_column :users, :admin, :boolean, default: false
  end
end
```

```ruby
$ rails c
$ User.all
$ user = User.find(3) ※ 任意のユーザに付与
$ user.update_attribute :admin, true
```

# rails_adminの日本語化

1. `config/locales/rails_admin.ja.yml`を作成

2. [この翻訳](https://gist.github.com/mshibuya/1662352) をコピーし、`rails_admin.ja.yml`に貼り付け

# 参考

[rails_admin - 公式Github](https://github.com/railsadminteam/rails_admin)

[初学者のメモ　Rails_adminの導入方法（日本語化） - qiita](https://qiita.com/mailok1212/items/8e36a5a10f19023bb0c4)

[RailsAdminと遊ぼう~カスタマイズ戦記~ - qiita](https://qiita.com/yuko-tsutsui/items/8f016c5cd1986a8f2ea3)

[deviseとcancancanで会員登録と権限管理を行い、管理者だけにrails_adminを公開する - qiita](https://qiita.com/iamdaisuke/items/79d60b3c23e465ae6460)

[[初心者向け] Railsで管理ページを作成し、管理者権限を持つユーザーのみアクセス可能にする[rails_admin] - qiita](https://qiita.com/daisuke114/items/4f6c7eb9a3a96ad1da54)

