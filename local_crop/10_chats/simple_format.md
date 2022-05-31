# simple_formatの使い方

- 文字列を`<p>`でくくる
- 改行は`<br />`を付与
- 連続した改行は、`</p><p>`を付与

# 使用例

```ruby
<% text = "テキスト\nテキスト\n\nテキストテキスト" %>
<%= simple_format text %>
```

出力結果
```ruby
<p>テキスト
<br />テキスト</p>

<p>テキストテキスト</p>
```

# タグが埋め込まれている場合

**タグが埋め込まれている場合はsimple_formatを使わないとエスケープされない。**

```ruby
<% text = "<h1>テキスト\nテキスト\n\nテキストテキスト</h1>" %>
<%= text %>
```

出力結果
```ruby
&lt;h1&gt;テキスト
テキスト

テキストテキスト&lt;/h1&gt;
```

表示結果
[![Image from Gyazo](https://i.gyazo.com/e7fc717d5c6fc9801ab5fb7684bb95a5.png)](https://gyazo.com/e7fc717d5c6fc9801ab5fb7684bb95a5)

# エスケープされない原因

```ruby
def simple_format(text, html_options = {}, options = {})
  wrapper_tag = options.fetch(:wrapper_tag, :p)

  text = sanitize(text) if options.fetch(:sanitize, true)
  paragraphs = split_paragraphs(text)

  if paragraphs.empty?
    content_tag(wrapper_tag, nil, html_options)
  else
    paragraphs.map! { |paragraph|
      content_tag(wrapper_tag, raw(paragraph), html_options)
    }.join("\n\n").html_safe
  end
end
```
simple_formatでは、`html_safe`で処理されている。

# 参考

[rails - 公式Github](https://github.com/rails/rails/blob/0e50b7bdf4c0f789db37e22dc45c52b082f674b4/actionview/lib/action_view/helpers/text_helper.rb#L283)

[simple_formatの使い方 - qiita](https://qiita.com/mojihige/items/c01682774e8ef29b361f)
