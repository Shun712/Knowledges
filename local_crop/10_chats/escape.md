# エスケープ処理を行う

エスケープとは、**HTML上で特殊文字を期待通りに表示する**ために施す処理のこと。  
例えば、`<`は`&lt;`であったり、`©`は`&copy;`など、特殊文字には必ず該当する記号が割りてられている。

# 実行例

```html
<html>
  <head>
    <title></title>
    <meta charset="utf-8" />
  </head>
  <body>
    <strong>この文字列は太くなります。</strong>
    <br />
    &lt;strong&gt;この文字は太くなりません。&lt;/strong&gt;
    <br />

    <h1>よく使う特殊記号</h1>

    &amp;(アンパサンド)
    <br />
    &lt;(小なり)
    <br />
    &gt;(大なり)
    <br />
    &quot;(ダブルクォーテーション)
    <br />
    &#39;（シングルクォーテーション）
    &nbsp;（空白）
    <br />
    &copy;（コピーライト）
  </body>
</html>
```

### 表示結果
[![Image from Gyazo](https://i.gyazo.com/b7dbde6bfb1a5683a6dd1260a484163a.png)](https://gyazo.com/b7dbde6bfb1a5683a6dd1260a484163a)

### 解説

次のコードはHTMLでstrongタグが適用されるため、太字で表示される。

```html
<strong>この文字列は太くなります。</strong>
```

次のコードは`&lt;`や`&gt;`がエスケープ処理されるため、`strong`が文字列で表示されるだけで、太字にはならない。

```html
&lt;strong&gt;この文字は太くなりません。&lt;/strong&gt;
```

# 参考

[TMLで特殊文字のエスケープ処理を行う方法【初心者向け】](https://techacademy.jp/magazine/12553)