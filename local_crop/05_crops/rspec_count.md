# RSpecで複数の同一要素の個数を数える方法

`page.all(.hoge.fuga)`で戻り値が配列になるのでその要素を数える。

# 具体例

`.card`という要素がページに2つあるとする。
`expect(page.all(".card").count).to eq 2`

「2つ目の要素をクリックする」
`page.all(".card")[1].click`

# 補足
変数に格納しておくと、複数箇所で使い回せる。
`crop_count =page.all(".card").count`

# 参考

[RSpec (Capybara) で複数の同一要素の個数を数えたり特定したりする方法](https://obel.hatenablog.jp/entry/20210319/1616095800)