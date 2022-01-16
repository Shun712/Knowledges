- turbolinksとは？
Rails4から正式導入された画面遷移を高速化させるライブラリである。
Railsではデフォルトでgemとして組み込まれている。

- 仕組み
turbolinksにおいて、リンクからページ表示までの一連の流れを**Visit**と呼ぶ。
  - Application Visits = リンククリックによるページ遷移
  - Restoration Visits = ブラウザの戻る/進むボタンによるページ遷移

- Application Visitの挙動
1. 同じドメイン内にリンクする<a href>タグのクリックを監視する
2. クリック時、リンクによるページ遷移を妨害する
3. キャッシュが存在する場合、その内容を一時的にbody上に表示する(キャッシュプレビュー表示)
4. Ajax(XMLHttpRequest)で次のページを取得する
5. 取得したページを、現在のページと置換える
  - <head>はマージする
  - <body>は完全に差し替える
6. スクロール位置を更新する
7. HistoryAPIを操作して、URLを変える(history.pushState.ページ遷移したように見せる)

- Restoration Visitsの挙動
1. キャッシュが存在する場合は、リクエストを出すことなくページを再表示させる
2. スクロール位置は記録されており、遷移時に復元される

### 参考
[6. Turbolinks](https://www.techscore.com/tech/Ruby/rails-4.0/turbolinks/)
[turbolinksチートシート](https://qiita.com/morrr/items/54f4be21032a45fd4fe9)
[【Rails】初心者向け！画面遷移の高速化を行うTurbolinksについて図を用いて詳しく解説](https://techtechmedia.com/turbolinks-rails/)