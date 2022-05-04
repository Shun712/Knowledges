# ActiveStorageを使ったFactoryBot作成

seedデータの作成と同じようにインスタンスを作成してから画像を追加する。

```ruby
FactoryBot.define do
  factory :crop do
    name { Faker::Food.vegetables }
    description { Faker::Hacker.say_something_smart }
    harvested_on { Date.today }
    association :user, factory: :user, strategy: :create

    after(:build) do |crop|
      crop.picture.attach(io: File.open('spec/fixture/files/test.png'), filename: 'test.png')
    end
  end
end
```

# 参考

[Active Storage 導入環境下での単体テスト - qiita](https://qiita.com/maca12vel/items/ee4d16827f24f69080ae)