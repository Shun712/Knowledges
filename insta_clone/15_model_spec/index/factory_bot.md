# FactoryBotとは?
テスト用データの作成をサポートするgemである。`ActiveRecord`モデルに実装したコールバックなどの資産を直接的に活用してデータの状態やデータ間の関係性などを制御しやすくなる。

# 実装手順

### 1. gemをインストール
```ruby
group :development, :test do
  gem 'factory_bot_rails'
end
```

### 2. ファイル生成
`$ bin/rails g factory_bot:model user`

### 3. サンプルコード
(spec/factories/users.rb)
```ruby
FactoryBot.define do
  factory :user do
    email { Faker::Internet.unique.email }
    password { '12345678' }
    password_confirmation { '12345678' }
    username { Faker::Name.name }
  end
end
```

### 4. 設定

テストコードから`FactoryBot`を省略してテータを生成できるようになる。  

(spec/support/factory_bot.rb)
```ruby
RSpec.configure do |config|
  config.include FactoryBot::Syntax::Methods
end
```

### 5. 画像のFactoryBot

アソシエーションを定義する場合、association元のモデル名を書くだけで良い。  
imagesは、gemに関わる公式wikiを見ると色々書いてある。
```ruby
FactoryBot.define do
  factory :post do
    body { Facker::Hacker.say_something_smart }
    images { [File.open("#{Rails.root}/spec/fixtures/fixture.png")] }
    user
  end
end
```

### 6. traitを使ったDRY
ファクトリを入れ子状にすることで継承できる。  
任意の属性だけ書き換えられる。

```ruby
FactoryBot.define do
  factory :project do
    sequence(:name) { |n| "Project #{n}" }
    description "A test project."
    due_on 1.week.from_now
    association :owner

    # 昨日が締め切りのプロジェクト
    trait :due_yesterday do
        due_on 1.day.ago
    end
  end
end

# 呼び出し方
let{:project} { create(:project, :due_yesterday) }
```

# 参考

[FactoryBot - Github](https://github.com/thoughtbot/factory_bot/blob/master/GETTING_STARTED.md#defining-traits)

[チートシート](https://github.com/brennovich/cheat-ruby-sheets/blob/master/factory_bot.md)

[Factorybotを使ったテストデータの作成方法 - qiita](https://qiita.com/righteous/items/e5448cb2e7e11ab7d477)

[RailsアプリへのRspecとFactory_botの導入手順 - qiita](https://qiita.com/Ushinji/items/522ed01c9c14b680222c)

[【ruby】Railsでファイルアップロードをテストする](https://tanihiro.hatenablog.com/entry/2014/01/09/004022)