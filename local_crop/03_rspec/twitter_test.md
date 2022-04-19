# click_buttonの使い方

RSpecでページ内のボタンをclickしてくれるのが`click_button`である。

# RSpecでclick_buttonが使える範囲

`describe`や`context`ブロック内では使えない。  
`it`内や`before`内では使用できる。

# 発生するエラー

```ruby
click_button` is not available on an example group (e.g. a `describe` or `context` block).  
It is only available from within individual examples (e.g. `it` blocks) or from constructs that run in the scope of an example (e.g. `before`, `let`, etc).
```

# 他のclickツール

`find().click`

クリックしたい場所のinput要素とname属性を探して()の中に書く。  
`find(‘input[name=“commit”]’).click`


# 参考

[Rails.Rspecにおける click_on find().clickなどの使い分け - qiita](https://qiita.com/pipi_nippi/items/d1f4fcb977640f086f84)