# システムスペックで日付・時刻フォームを入力する

フォームに入力するためには、ヘルパーを定義してRSpecで利用する。

# ビューの作成

```ruby
< %= f.label :start_at, "開始時間" %>
<%= f.datetime_select :start_at % >
```

上記のフォームを定義すると、   
id="モデル名_start_at_1i" (年を入力)  
id="モデル名_start_at_2i" (月を入力)  
id="モデル名_start_at_3i" (日を入力)  
id="モデル名_start_at_4i" (時を入力)  
id="モデル名_start_at_5i" (分を入力)  
というIDを持つフィールドが作成される。

# ヘルパーを作成

フィールドに値を入力するようなヘルパーを作成する。

```ruby
# spec/support/select_date_helper.rb

module SelectDateHelpers
  def select_date(date, options = {})
    field = options[:from]
    base_id = find(:xpath, ".//label[contains(.,'#{field}')]")[:for]
    year, month, day = date.split('-')
    select year, :from => "#{base_id}_1i"
    select month, :from => "#{base_id}_2i"
    select day, :from => "#{base_id}_3i"
  end

  def select_time(hour, minute, options = {})
    field = options[:from]
    base_id = find(:xpath, ".//label[contains(.,'#{field}')]")[:for]
    select hour, :from => "#{base_id}_4i"
    select minute, :from => "#{base_id}_5i"
  end
end
```

# 設定

`rails_helper`で以下のコードがコメントインされていることを確認

```ruby
# spec/rails_helper.rb

Dir[Rails.root.join('spec', 'support', '**', '*.rb')].each { |f| require f }
```

ヘルパーをincludeする。

```ruby
# spec/rails_helper.rb

RSpec.configure do |config|
  ︙
  config.include SelectDateHelpers
end
```

# 実装例

```ruby
context '入力情報が正しい場合' do
  it '新規登録できること' do
    attach_file 'crop[picture]', "#{Rails.root}/spec/fixture/files/test.png"
    fill_in '作物名', with: 'トマト'
    fill_in '説明', with: 'テスト説明'
    select_date('2022-5-4', from: '収穫日')
    click_button '登録する'
    expect(current_path).to eq crops_path
    expect(page).to have_content '作物を登録しました'
  end
end
```

# 参考

[【RSpec】テストの際、日付・時刻フォーム(datetime_select)に値を入力する - qiita])(https://qiita.com/Tatty/items/be8b7afecad47da168ca)