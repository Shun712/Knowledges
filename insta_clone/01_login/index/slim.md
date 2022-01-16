- slimには閉じタグという概念がない。代わりにインデントを使い、マークアップする範囲を指定する。また、インデントの深さは自由だが、2スペース開けた場合は、その後も2スペースにする必要がある。

- テキストの書き方
```
p
  |  サンプル
```
```
<p>サンプル</p>
```

- 長いテキストを書く場合と改行
```
p
  |
    明日の天気予報は<br>
    晴れ時々くもりです。
```
- 属性の書き方
```
a href='http://www.sample.com' サンプル
```
```
<a href="http://www.sample.com">サンプル</a>
```

- pタグの中にspanタグを使う
`左の文字(間)右の文字`を表示する
```
p
  | 左の文字(
  span
    | 間
  | )右の文字
```

- IDとclassの書き方
```
#sample
  サンプル
div.sample
  サンプル
.sample
  サンプル
```
```
<div id="sample">サンプル</div>

<div class="sample">サンプル</div>

<div class="sample">サンプル</div>
```

- 複数定義する
```
#sample.hoge.fuga
  サンプル
.sample.hoge
  サンプル
```
```
<div id="sample" class="hoge fuga">サンプル</div>

<div class="sample hoge">サンプル</div>
```

# 参考
[【Rails】 slimの書き方をマスターしよう！](https://pikawaka.com/rails/slim)