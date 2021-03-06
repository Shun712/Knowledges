# メール認証をつけたスペックテストの実装

### 1. factory_botでデータを作成

`after(:create) { |user| user.confirm }`によって`user = create(:user)`と書いた時に自動でアカウントが有効化される。

```ruby
# spec/factories/users.rb

FactoryBot.define do
  factory :user do
    username { Faker::Name.name }
    email { Faker::Internet.unique.email }
    password { 'testpassword' }
    password_confirmation { 'testpassword' }
    # createのときは自動でconfirm
    after(:create) { |user| user.confirm }
  end
end
```

### 2. config/environments/test.rbを編集

```ruby
config.action_mailer.default_url_options = { :host => 'localhost:3000' }  #これを追加。
```

### 3. モデルスペックを実装

```ruby
RSpec.describe User, type: :model do
  let(:user) { create(:user) }

  context "バリデーション" do
    it "名前、メールアドレスがあれば有効な状態であること" do
      expect(user).to be_valid
    end

    it "名前がなければ無効な状態であること" do
      user = build(:user, username: nil)
      user.valid?
      expect(user.errors[:username]).to include("を入力してください")
    end

    it "メールアドレスがなければ無効な状態であること" do
      user = build(:user, email: nil)
      user.valid?
      expect(user.errors[:email]).to include("を入力してください")
    end

    it "重複したメールアドレスなら無効な状態であること" do
      other_user = build(:user, email: user.email)
      other_user.valid?
      expect(other_user.errors[:email]).to include("はすでに存在します")
    end

    it "メールアドレスは小文字で保存されること" do
      email = "ExamPle@example.com"
      user = create(:user, email: email)
      expect(user.email).to eq email.downcase
    end

    it "パスワードがなければ無効な状態であること" do
      user = build(:user, password: nil)
      user.valid?
      expect(user.errors[:password]).to include("を入力してください")
    end

    it "パスワードは6文字以上であること" do
      password = "a" * 5
      user = build(:user, password: password)
      user.valid?
      expect(user.errors[:password]).to include("は6文字以上で入力してください")
    end
  end
end
```

# 参考

[devise - 公式github](https://github.com/heartcombo/devise/wiki/How-To:-Test-controllers-with-Rails-(and-RSpec))

[[Rspec]Deviseでメール認証をつけてる時のテストの書き方 - qiita](https://qiita.com/RI5255/items/f55cd04ca1f3b7b5be50)