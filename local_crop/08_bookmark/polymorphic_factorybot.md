# FactoryBotでポリモーフィックなアソシエーションを生成

一般のUserの他に別テーブルで管理されてるCompanyも投稿できる設計とする。

```
User ----|
         |---- Post
Company--|
```

```ruby
# factories/posts.rb

# userのpostを生成(postと一緒にuserができる)
FactoryBot.define do
  factory :user_post, class: 'Post' do
    postable_type { 'User' }
    #ポリモーフィック関連の名前を指定して、userを生成するfactorを呼ぶ
    association :postable, factory: :user
  end

# companyのpostを生成(postと一緒にcomapnayができる）
  factory :company_post, class: 'Post' do
    postable_type { 'Company' }
    #ポリモーフィック関連の名前を指定して、userを生成するfactorを呼ぶ
    association :postable, factory: :company
  end
end
```

# 参考

[FactoryBotでポリモーフィックなアソシエーションを生成する - qiita](https://qiita.com/Paul_Dirac/items/5242f2a030a88ca159f1)