# 複数のテストデータを作成する

ページネーションをテストするのにデータが複数必要になるので簡単にテストデータを取得する。

# 使い方

ファクトリでデータを定義する

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

複数定義したい場合は以下のようにit節内で設定する。  
データを作成した後は、**ページ更新しなければ表示されない**。

```ruby
it 'ページネーションボタンが表示されること' do
  create_list(:crop, 30)
  # create_listした後はページ更新しなければ作成されない
  visit crops_path
  expect(page).to have_css('.page-link')
  expect { find_link('2', rel = "next").click }
  expect { find_link('1', rel = "prev").click }
end
```

# オプション

```ruby
# 変数articlesに3つのtaskインスタンスの配列が入っている
articles = create_list(:article, 3)
```


```ruby
# :doingはtrait、titleは上書き
articles = create_list(:article, 3, :doing, title: 'new_title')
```

# 参考

[【FactoryBot】create_listで複数のインスタンスの配列を作成する【RSpec】 - qiita](https://qiita.com/kikikikimorimori/items/5e91fbd7e088f3b9d4a4)

[factory_bot - create_listメソッドの使い方](https://forest-valley17.hatenablog.com/entry/2018/09/29/151009)