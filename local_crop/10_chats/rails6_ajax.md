# Rails6でのAjaxを実装

Rails 6.1から仕様が変わり、`local: true` がデフォルトになった。  
`js.erb` を呼び出すには `local: false` が必要となる。

# 非同期の設定

- HTMLに`data-remote="true"` が**含まれていない**場合は`create.html.erb`を呼び出すには、`local: true`オプションが必要。  
- `data-remote="true"` が**含まれている**場合は、自動的に `Ajax` を利用して非同期通信（ページ遷移無しに通信）が行われ、`create`メソッドが実行される。さらに指示がない場合、`create.js.erb`が呼び出される。非同期で呼び出されない場合は、`local: false`オプションが必要である。

# 参考

[3.1 remote要素 - Railsガイド](https://railsguides.jp/working_with_javascript_in_rails.html#remote%E8%A6%81%E7%B4%A0)

[【Rails 6】（初心者向け）Ajax版最小構成CRUDアプリ（ページ移動をゼロに！）- qiita](https://qiita.com/take18k_tech/items/7d4917e30d4c879701ef#1%E3%83%A1%E3%83%83%E3%82%BB%E3%83%BC%E3%82%B8%E3%81%AE%E4%BD%9C%E6%88%90)