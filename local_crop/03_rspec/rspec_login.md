# RSpecでログイン状態にする方法

deviseではユーザーをログイン状態にするヘルパーメソッドが用意されている。

```ruby
require 'rails_helper'

RSpec.describe 'UserSessions', type: :system do
  let(:user) { create(:user) }

  describe 'ログアウト' do
    before do
      sign_in user
      visit root_path
    end
    it 'ログアウトできること' do
      click_on('ログアウト')
      expect(current_path).to eq new_user_session_path
      expect(page).to have_content('ログアウトしました。')
    end
  end
end
```

# sign_inメソッドを使わずにログイン状態にする方法

> System spec は基本的に結合テストでブラックボックステストなので、内部実装 ( sign_in のようなメソッドを使わずにテストするものかと思います。
> 
> [system test で devise の sign_in メソッドを使いたい - teratail](https://teratail.com/questions/280085)

```ruby
before do
  visit new_user_session_path
  fill_in 'メールアドレス', with: user.email
  fill_in 'パスワード', with: 'testpassword'
  click_button 'ログイン'
end
```

# 参考

[devise - 公式github](https://github.com/heartcombo/devise/blob/f8d1ea90bc328012f178b8a6616a89b73f2546a4/lib/devise/controllers/sign_in_out.rb#L108)

[RSpecでログイン状態にする方法(sign_inヘルパー) - qiita](https://qiita.com/qp___04/items/084ded235ea109fc90fb)

[system test で devise の sign_in メソッドを使いたい - teratail](https://teratail.com/questions/280085)