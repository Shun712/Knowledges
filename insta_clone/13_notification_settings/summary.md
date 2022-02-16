# 13 通知の設定を実装

# やったこと
- 通知をするかしないかをユーザーが設定できる機能を実装
- マイページに通知設定というメニューを追加
- コメント時の通知メール, いいね時の通知メール, フォロー時の通知メールのオンオフを切り替えられるようにする

# 学んだこと
- `form_with`の復習をしてみた。

```html
= form_with model: @user, url: mypage_notification_setting_path, method: :patch, local: true do |f|
  = render 'shared/error_messages', object: f.object
  .form-group
    = f.check_box :notification_on_comment
    = f.label :notification_on_comment

  .form-group
    = f.check_box :notification_on_like
    = f.label :notification_on_like

  .form-group
    = f.check_box :notification_on_follow
    = f.label :notification_on_follow

  = f.submit class: 'btn btn-primary btn-raised'

```
`form_with`はHTMLとして以下のように出力される。
```html
<form action="/mypage/notification_setting" accept-charset="UTF-8" method="post">
    <input name="utf8" type="hidden" value="✓">
    <input type="hidden" name="_method" value="patch">
    <input type="hidden" name="authenticity_token" value="wQEP4lPAVkdV7MNomZOODoQIfiBbcrNd5+B2N1mNxvqylMgzr1KvxuQ2bFtAOsNlx+TGQ9WWGtebS+C/+56esA==">
    <div class="form-group">
        <input name="user[notification_on_comment]" type="hidden" value="0">
        <input type="checkbox" value="1" checked="checked" name="user[notification_on_comment]" id="user_notification_on_comment">
        <label for="user_notification_on_comment">コメント時の通知メール</label>
    </div>
    <div class="form-group">
        <input name="user[notification_on_like]" type="hidden" value="0">
        <input type="checkbox" value="1" checked="checked" name="user[notification_on_like]" id="user_notification_on_like">
        <label for="user_notification_on_like">いいね時の通知メール</label>
    </div>
    <div class="form-group">
        <input name="user[notification_on_follow]" type="hidden" value="0">
        <input type="checkbox" value="1" name="user[notification_on_follow]" id="user_notification_on_follow">
        <input type="submit" name="commit" value="更新する" class="btn btn-primary btn-raised" data-disable-with="更新する">
        <label for="user_notification_on_follow">フォロー時の通知メール</label>
    </div>
</form>
```
- modelオプションを使う場合、`form_with`の引数にはモデルクラスのインスタンスを指定する。
- 今回の場合は、通知設定のため`updateアクション`が動くパスに変換されるが、ユーザー登録や編集の場合は、インスタンスの有無で`createアクション`か`updateアクション`を自動的に振り分けてくれる。
- urlオプションを指定しない場合
```html
<form action="/users/31" accept-charset="UTF-8" method="post">
```
- urlオプションを指定する場合
```html
<form action="/mypage/notification_setting" accept-charset="UTF-8" method="post">
```
urlオプションはHTMLに出力すると、form要素のaction属性に変換され、送信されるデータの送信先を指定する。urlオプションを指定しないと、ユーザーの個別IDを送信先にされてしまうが、今回の通知設定は名前空間の`mypage`にしているのでルーティングエラーが発生してしまうため、urlオプションを指定する必要がある。
- 上記でチェックした通知設定(form要素に`name="user[notification_on_comment]" `としてsubmitされたデータ)は、リクエストパラメータとしてリクエストに添えて送られる。
  このリクエストパラメータは、コントローラーにおいてparamsメソッドを利用して、取得する。