# 16 システムスペックを実装
## やったこと
システムスペックを書く。

- ログイン成功/失敗
- ログアウトできる
- ユーザー登録成功/失敗
- フォローできること
- フォローをはずせること
- 投稿一覧が閲覧できる
- 新規投稿できる
- 自分の投稿に編集・削除ボタンが表示される
- 他人の投稿には編集・削除ボタンが表示されない
- 投稿を更新できる
- 投稿を削除できる
- 投稿の詳細画面が閲覧できる
- 投稿に対していいねできる
- 投稿に対していいねを外せる

## システムスペック
ユーザーの立場に立って、想定通りの画面操作が行えるかどうかテストする。
例えば、リンクをクリックして、フォームに値を入力するなどの操作を一つ一つ行いながらテストする。
実行速度や保守性の問題を抱えているので、正常系のテスト等に限定することが多い。

## Capybara
Webアプリケーションのブランチ操作をシミュレーションできるほか、実際のブラウザと組み合わせてJavaScriptの動作まで含めたテストを行うことができる。

## webdrivers
Chromeとやりとりするのに必要なChromeDriverを含む。

## 詰まったこと
```ruby
1) ユーザー登録 フォロー フォローできること
     Failure/Error: = link_to "確認する", user_url(@user_from)

     ActionView::Template::Error:
       Missing host to link to! Please provide the :host parameter, set default_url_options[:host], or set :only_path to true
```
`ActionMailer`を経由しているので、test環境ではhostパラメータを定義し忘れていたためにエラーが発生していた。
> [パスワードリセットのシステムテストをしていたら、Rails Missing host to link to! のエラーがおでましになった - qiita](https://qiita.com/vinaka/items/aa40d1c70535b8bc7253)
