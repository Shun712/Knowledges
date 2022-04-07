# SNSとOAuth連携の実装

Deviseというgemのominauthableを利用して、SNS連携を実現する。

# 実装手順

### 1. gemのインストール

```ruby
# Gemfile
gem 'omniauth', '~> 1.9.1'
gem 'omniauth-line'
gem 'omniauth-twitter'
gem 'omniauth-rails_csrf_protection'
```
`gem 'omniauth-rails_csrf_protection'`はセキュリティの脆弱性対策として必要。

### 2. 各providerのOAuth設定

各providerにOAuthを申請して、`AccessKey`と`AccessSecret`を得る。  
githubに公開しないように.envファイルで管理する。
```ruby
# .env
LINE_KEY = 'アクセスキー'
LINE_SECRET = 'シークレットキー'

TWITTER_KEY = 'アクセスキー'
TWITTER_SECRET = 'シークレットキー'

DOMAIN_NAME = 'http://localhost:3000/'
```

### 3. 各サービスでどういった譲歩を取得するか設定

```ruby

Devise.setup do |config|
  # ==> OmniAuth
  # Add a new OmniAuth provider. Check the wiki for more information on setting
  # up on your models and hooks.
  # config.omniauth :github, 'APP_ID', 'APP_SECRET', scope: 'user,public_repo'
  config.omniauth :line, ENV['LINE_KEY'], ENV['LINE_SECRET']
  config.omniauth :twitter, ENV['TWITTER_KEY'], ENV['TWITTER_SECRET'], scope: 'email', oauth_callback: "#{ENV['DOMAIN_NAME']}/users/auth/twitter/callback"
end
```

### 4. Modelの設計

それぞれのproviderに対し、統一的に扱えるよう`SocialProfile`というモデルを作成する。  
oauthの結果には、`provider`と各ユーザーを識別するID`:uid`が確実に含まれる。  
念のため`credentials`の情報と`raw_info`の情報をJSON形式で保存しておけば、もし何か保存し忘れた時も復元できる。

```ruby
# app/models/social_profile.rb
class SocialProfile < ApplicationRecord
  belongs_to :user
  validates :uid, uniqueness: { scope: :provider }

  def set_values(omniauth)
    # すでに同providerで認証済みか条件分岐する。
    # 認証済みならreturn
    return if provider.to_s != omniauth['provider'].to_s || uid != omniauth['uid']

    credentials = omniauth['credentials']
    info = omniauth['info']

    access_token = credentials['refresh_token']
    access_secret = credentials['secret']
    credentials = credentials.to_json
    name = info['name']
    # self.set_values_by_raw_info(omniauth['extra']['raw_info'])
  end

  def set_values_by_raw_info(raw_info)
    self.raw_info = raw_info.to_json
    save!
  end
end
```

`$ rails g model SocialProfile user:references provider uid`

```ruby
# app/models/user.rb
class User < ActiveRecord::Base
  devise :omniauthable

  has_many :social_profiles, dependent: :destroy
  def social_profile(provider)
    social_profiles.select{ |sp| sp.provider == provider.to_s }.first
  end
end
```

### 5. ルーティングとコントローラ設定
```ruby
# config/routes.rb
Rails.application.routes.draw do
  # Deviseのマッピングはするが、skipして何も設定しない
  devise_for :users, controllers: {
               omniauth_callbacks: 'users/omniauth_callbacks',
  }
end
```

```ruby
# app/controllers/users/omniauth_callbacks_controller.rb
class Users::OmniauthCallbacksController < Devise::OmniauthCallbacksController
  def line
    basic_action
  end

  def twitter
    basic_action
  end

  private

  def basic_action
    # request.env['omniauth.auth']の中に受け取ったデータが入っている。
    @omniauth = request.env['omniauth.auth']
    if @omniauth.present?
      # SocialProfilesのレコードがある場合はサインイン、ない場合はサインアップに飛べる
      @profile = SocialProfile.where(provider: @omniauth['provider'], uid: @omniauth['uid']).first
      if @profile
        # set_valuesメソッドで、トークンなどの情報を保存することができる
        @profile.set_values(@omniauth)
        sign_in(:user, @profile.user)
      else
        @profile = SocialProfile.new(provider: @omniauth['provider'], uid: @omniauth['uid'])
        # ランダムのemailを作成しておりますが、ユーザーのレコードを作成したときの条件分岐のところはユーザーの編集画面に飛ばすなどの工夫も必要
        email = @omniauth['info']['email'] || Faker::Internet.email
        @profile.user = current_user || User.create!(email: email, username: @omniauth['info']['name'], password: Devise.friendly_token[0, 20])
        @profile.set_values(@omniauth)
        sign_in(:user, @profile.user)
      end
    end
    redirect_to root_path, success: 'ログインしました。'
  end
end
````

> LINE Loginは調べるとemail情報を取ってくることができないらしいので、SNSのアカウント毎にユーザーを作るようにします。
> [【Rails4, OmniAuth】世界一丁寧なLINE LOGIN導入講座](https://qiita.com/YuitoSato/items/a9e613370f418d5c322c)

# 6. ビューの設定
```ruby
# app/views/devise/sessions/new.html.slim
- resource_class.omniauth_providers.each do |provider|
                = link_to omniauth_authorize_path(resource_name, provider), method: :post, class: "btn-social bs-#{provider} me-2 mb-2" do
                  i.fa-brands.fa-2x class="fa-#{provider}"
```

# 参考

[omniauth-line - 公式Github](https://github.com/kazasiki/omniauth-line)

[omniauth-twitter - 公式Github](https://github.com/arunagw/omniauth-twitter)

[【画像付き】RailsでDeviseを利用してLINEログイン機能を実装 - qiita](https://qiita.com/s10aim_tana/items/2d174d4e31e4041700ee)

[【Rails4, OmniAuth】世界一丁寧なLINE LOGIN導入講座 - qiita](https://qiita.com/YuitoSato/items/a9e613370f418d5c322c)

[Rails5系でLineログインを実装する](https://techdatebook.hatenablog.com/entry/rails_line)

[RailsでいろんなSNSとOAuth連携/ログインする方法 - qiita](https://qiita.com/awakia/items/03dd68dea5f15dc46c15)

[DeviseとOmniauthでtwitter,facebook ログイン機能 - qiita](https://qiita.com/sakakinn/items/321e6b49c92b9f02f83f)

[RailsにDevise+OmniAuthでユーザ認証を実装する手順 - qiita](https://qiita.com/zenizh/items/94aec2d94a2b4e9a1d0b)

[【開発メモ】RailsアプリにTwitterログイン認証機能を実装する方法](https://freesworder.net/rails-twitter/)
