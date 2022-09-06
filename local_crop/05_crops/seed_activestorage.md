# 基本的な書き方(carrierwaveを使用)

```ruby
User.limit(30).each do |user|
  crop = user.crops.create(name: Faker::Food.vegetables,
                           description: Faker::Hacker.say_something_smart,
                           harvested_on: Faker::Date.between(from: 3.days.ago, to: Date.today),
                           remote_images_urls: %w[https://picsum.photos/350/350/?random https://picsum.photos/350/350/?random])
  puts "crop#{crop.id} has created!"
end
```

# ActiveStorageを使用したseedデータ作成

ファイルの登録にActiveStorageを使っている場合、以下のように記述する。  
画像に`null: false`のバリデーションを付与しているのでインスタンスの作成してから画像を添付している。

```ruby
User.limit(3).each do |user|
  crop = user.crops.new(name: Faker::Food.vegetables,
                        description: Faker::Hacker.say_something_smart,
                        harvested_on: Faker::Date.between(from: 3.days.ago, to: Date.today)
  )
  crop.picture.attach(io: File.open(Rails.root.join('app/assets/images/400x200-crop-dummy.png')), filename: 'test.png')
  crop.save!
end
```

# 参考

[FactoryBot　ActiveStorageを使った画像を紐付ける方法 - qiita](https://qiita.com/minisera/items/c78759634a256a0b98c3)

[【Rails】マイグレーションの書き方《Seed篇》](https://www.autovice.jp/articles/121)

[【Rails】seeds.rbでサンプルデータ作成時に画像も一緒に生成する（ActiveStorage使用） - qiita](https://qiita.com/4ma9147/items/567f90194d169a23c729)