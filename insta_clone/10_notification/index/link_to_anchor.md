# link_toのanchorオプションとは?

リンク先にページ遷移をした際、場所(位置)を指定することができる。

# 実装

```azure
<%= link_to 'リンクのテキスト', リンク先のページのpath(anchor: 'リンク先のページの途中のID'), class: 'aタグのクラス名' %>
```
遷移先の位置を指定するには、**ID**が必要である。

# 参考

[Rails アンカーリンクを使い遷移先ページの場所(位置)を指定する - qiita](https://qiita.com/hellhellmymy/items/37ce7197c8f206715af2)

[Rails でアンカー付きのリンクの書き方](https://machida.github.io/articles/20160712-anchorlink/)