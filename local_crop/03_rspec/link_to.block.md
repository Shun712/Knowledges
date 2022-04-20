# link_toのブロック使用時のエラー

link_toメソッドでブロックを使おうとした場合、`undefined method 'stringify_keys' for`というエラーが発生した。  
原因はnameとurlを両方使ってる場合はブロックは取れないからであった。

```ruby
= link_to 'ログアウト', destroy_user_session_path, class: 'nav-link', method: :delete do
  i.fa-solid.fa-arrow-right-from-bracket
```

リファレンス
```ruby
link_to(name = nil, options = nil, html_options = nil, &block)

link_to(body, url, html_options = {})
  # url is a String; you can use URL helpers like
  # posts_path

link_to(body, url_options = {}, html_options = {})
  # url_options, except :method, is passed to url_for

link_to(options = {}, html_options = {}) do
  # name
end

link_to(url, html_options = {}) do
  # name
end
```

# 解決方法

```ruby
= link_to destroy_user_session_path, class: "nav-link", method: :delete do
  i.fa-solid.fa-arrow-right-from-bracket
  |  ログアウト
```

# 参考

[link_toメソッドでブロック使おうとしたら"undefined method `stringify_keys' for"ってエラーが出る - qiita](https://qiita.com/drwtsn64/items/4e94caeaa392fbe4f289)