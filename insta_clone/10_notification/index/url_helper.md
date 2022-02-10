# URLヘルパーをビューやコントローラ以外の場所で使う

アプリケーションへのURLをビューやコントローラーの外で生成する必要があるときに、ルーティング用ヘルパーを用いれば、URLヘルパーを利用することができる。

# 実装

```ruby
class Activity < ApplicationRecord
  # URLヘルパーを使うため導入
  # これでモデルクラス内でURLを生成できる。
  include Rails.application.routes.url_helpers

  def redirect_path
    # selfが省略されている
    case action_type.to_sym
    when :commented_to_own_post
      post_path(subject.post, anchor: "comment-#{subject.id}")
    when :liked_to_own_post
      post_path(subject.post)
    when :followed_me
      user_path(subject.follower)
    end
  end
end
```

# 導入する意味

URLヘルパーが使われるのは、Webリクエストのコンテキスト、つまり**ビューやコントローラーの中**である。  
この場合は、リクエストの`host`やドメインは**アプリケーションが自動的**に提供する。  
ビューやコントローラーの外では、`_url`や`_path`で終わるヘルパーに`host`を明示的に提供する必要がある。  

例えば、`"http://hoge.com/user/1"` を取得したい場合、URLヘルパー(` include Rails.application.routes.url_helpers`)を導入しなければ、
モデル内で`user_path(user)`を設定しても
"/user/1"しか生成されない。


# 参考

[Rails: URLヘルパーをビューやコントローラ以外の場所で使う（翻訳）](https://techracho.bpsinc.jp/hachi8833/2021_03_05/104476)

[How to access URL helper from rails module - stack overflow](https://stackoverflow.com/questions/6074831/how-to-access-url-helper-from-rails-module)

[Railsの不特定ModuleやClass(Modelなど)で`_path`を使う - qiita](https://qiita.com/jerrywdlee/items/f91c9ea01055cb74083c)