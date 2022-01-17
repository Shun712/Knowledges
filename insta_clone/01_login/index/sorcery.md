# sorceryとは?

Railsに認証機能の実装を行うためのライブラリである。 同じように認証機能を提供してくれているものとして**devise**などが挙げられるが、**sorcery**の方がよりシンプルで、カスタマイズ性に富んでいる。
高機能の認証を手っ取り早く作りたいなら「devise」
少し面倒臭さは感じても、ある程度はロジックを自分で書いていきたい方は「sorcery」

# sorceryによってよく使うメソッド

1. `logged_in?`
ログインしているか有無で表示を変えたり、処理を変えたりする事ができる

2. `login`
ログインするためのメソッド。

3. `logout`
ログアウトするためのメソッド。

4. `redirect_back_or_to`
保存されたURLがある場合そのURLに、ない場合は指定されたURLにリダイレクトする。

5. `require_login`
ログインを強制する。

6. `not_authenticated`
ログインしていなかった場合に呼ばれるメソッド。以下のように実装する。

- ログインしていなかったらフラッシュメッセージを表示する

- ログインしていなかったらこのページにリダイレクトをする 

```
# app/controllers/application_controller.rb
private
def not_authenticated
  redirect_to login_path, alert: "ログインしてください"
end
```

# 参考
[【Rails】sorceryについて](https://boku-boc.hatenablog.com/entry/2020/10/10/213625)

[シンプル認証gem sorceryを完全入門するで！！](https://qiita.com/babashunsu/items/9937b0a2e08d318edece)