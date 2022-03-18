# rails_adminとは?

ActiveAdminとは、Modelに設定したパラメータを利用してCRUDをサポートする画面を作成できるgemである。
管理機能はDeviseとCancanの連携で実現できる。

# 導入手順

### 1. ActiveAdminのインストール

```
gem 'activeadmin'
gem 'devise'
```
`bundle install`

### 2. ActiveAdminに必要なファイルを作成

`bin/rails g active_admin:install`

`bin/rails db:migrate`

### 3. 初期データとしてログイン用のユーザを作成

`bin/rails db:seed`

### 4. モデルを作成

`bin/rails g model Author name:string`

`bin/rails db:migrate`

### 5. ビューを作成

`rails g active_admin:resource`コマンドにモデル名を渡すことで、そのモデルに対する管理ページを作成できる。

`bin/rails g active_admin:resource Author`

これで`app/admin/authors.rb`が作成され、ブラウザで確認できる。

このままリソースを新規作成すると`ActiveModel::ForbiddenAttributesError`が出るので`permit_params`を追加する。

```ruby
ActiveAdmin.register Author do
  permit_params :name
end
```

# 参考
[activeadmin - Github](https://github.com/activeadmin/activeadmin)

[Railsで最速で管理画面を作る！ - qiita](https://qiita.com/enomotodev/items/5f6d9348207124a41bf9)

[Active Admin 徹底解説 - qiita](https://qiita.com/MariMurotani/items/aed93986e29249fd65e5)
