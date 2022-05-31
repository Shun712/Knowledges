# html_safeメソッド

htmlタグをタグとして出力する

# 使用例

```html
<%= "test" %>
<%= "<br>".html_safe %>
<%= "test" %>
<%= "<br>" %>
<%= "test" %>
```

実行結果

```html
test
test<br>test
```

`html_safe`を使用しない場合は、以下のように`<br>`がそのまま出力される。

# 参考

[rails6 htmlタグをタグとして出力する](https://mebee.info/2021/11/10/post-32436/)