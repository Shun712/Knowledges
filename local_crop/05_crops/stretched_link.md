# Stretched link (ストレッチリンク)を理解する

CSSでリストされたリンクを`stretched-link`にすることで任意のHTML要素やBootstrapコンポーネントをクリックできるようにする。

# 実装

Bootstrapではデフォルトで`.card`に `position：relative`があるので他のHTMLを変更せずに、カード内のリンクに `.stretched-link`クラスを追加できる。  
複数のリンクやタップターゲットは、ストレッチリンクでは推奨されていない。

```html
<div class="card" style="width: 18rem;">
  <img src="..." class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Card with stretched link</h5>
    <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
    <a href="#" class="btn btn-primary stretched-link">Go somewhere</a>
  </div>
</div>
```

# 参考

[Stretched link (ストレッチリンク) - 公式bootstrap](https://getbootstrap.jp/docs/5.0/helpers/stretched-link/)