# deviseのコントローラをカスタマイズ

### 1. 完全に独自ロジックにしたい場合

deviseにデフォルトに用意されている機能を完全に独自のロジックにしたい場合、`super`の記述をコメントアウトする。

```ruby

class Users::RegistrationsController < Devise::RegistrationsController
  # GET /resource/sign_up
  def new
    super
  end

  # POST /resource
  def create
    #super
    独自ロジックを記述
  end
end
```

### 2. 一部分のみを独自のロジックにしたい場合

- カスタマイズしたいメソッドをgemファイルからコピー
- superメソッドをコメントアウトし、コピーしてきたメソッドを呼び出すようにする
- コピーしたいメソッドを独自に修正し、独自メソッドでカスタマイズする

```ruby

class Users::RegistrationsController < Devise::RegistrationsController
  def new
    super
  end

  def create
    # super
    devise_create
  end

  def devise_create
    build_resource(sign_up_params)

    resource.save
    yield resource if block_given?
    if resource.persisted?
      if resource.active_for_authentication?
        set_flash_message! :notice, :signed_up
        sign_up(resource_name, resource)
        respond_with resource, location: after_sign_up_path_for(resource)
      else
        set_flash_message! :success, :"signed_up_but_#{resource.inactive_message}"
        expire_data_after_sign_in!
        respond_with resource, location: after_inactive_sign_up_path_for(resource)
      end
    else
      clean_up_passwords resource
      set_minimum_password_length
      respond_with resource
    end
  end
end 
```

# deviseファイルは直接カスタマイズしてはいけない

gemは外部ライブラリのため、`bundle install`や`bundle update`するとファイルが上書きされ、編集した内容が消える可能性がある。  
また、外部ライブラリは一般的にgit管理しないので、gitで管理しているプロジェクトでは変更をコミットできない。

# 参考

[【Rails】deviseのコントローラを独自にカスタマイズする方法](https://toarurecipes.com/devise-customize/)