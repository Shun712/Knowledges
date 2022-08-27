# deviseでのリダイレクト先を設定

`app/controllers/users/registrations_controller.rb`に次の記載をすることで、情報更新時のリダイレクト先を指定できる。  

アカウント登録後に、アカウント編集ページへリダイレクトされる。

```ruby
# app/controllers/users/registrations_controller.rb

protected

  def after_sign_up_path_for
    edit_account_path
  end

end
```

# 参考

[【Rails/devise】アカウント情報編集機能の実装/リダイレクト先の変更手順 - qiita](https://qiita.com/saika_0/items/ae7c57e26037115ed2fc#3-%E6%9B%B4%E6%96%B0%E5%BE%8C%E3%81%AE%E3%83%AA%E3%83%80%E3%82%A4%E3%83%AC%E3%82%AF%E3%83%88%E5%85%88%E3%82%92%E5%A4%89%E6%9B%B4)