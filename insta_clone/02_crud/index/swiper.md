# swiperとは?

SwiperはJavaScriptライブラリで、JQueryに依存せずJavaScript単体で動作させることができ、CSSとJSを適用することで、画像などをスライドできる機能。

公式サイトでどのように実装できるか紹介されている。

> [Swiper公式サイトのデモ](https://swiperjs.com/get-started)

# 実装手順

### 1. HTML(slim)の実装

```
/! Slider main container
.swiper
  /! Additional required wrapper
  .swiper-wrapper
    /! Slides
    .swiper-slide Slide 1
    .swiper-slide Slide 2
    .swiper-slide Slide 3
    | \...
  /! If we need pagination
  .swiper-pagination
  /! If we need navigation buttons
  .swiper-button-prev
  .swiper-button-next
  /! If we need scrollbar
  .swiper-scrollbar

```

Swiperが用意している`swiper-wrapper`クラスや
`swiper-slide`クラスなどに適用するためのコードが用意されている。

`/! If we need...`はオプション部分である。

### 2. CSS、JSの適用方法

公式サイトでは、3パターン紹介されている。

- CDN（クラウド上に公開されているCSSとJSを適用させる）

- ファイルをダウンロードして、愚直にCSSとJSを適用させる

- NPMというJSのパッケージマネージャ（RubyでいうところのGemを管理するBundlerのようなもの）

    - Yarnという類似のパッケージマネージャーを使うことも可能

### 2.1. CDNでの設定方法

#### CDNとは?

CDNとは「Content Delivery Network（コンテンツデリバリーネットワーク）」の略で、アクセスが集中したりコンテンツ(ここではSwiper)が大容量化したりしても、ホームページの表示やコンテンツの配信に問題が起こらないようにすることが可能である。

#### 設定方法

```
<!DOCTYPE html>
<html lang="ja">
<head>
    ...
   <link rel="stylesheet" href="https://unpkg.com/swiper@7/swiper-bundle.min.css"/>
</head>

<body>
    ...
    <script src="https://unpkg.com/swiper@7/swiper-bundle.min.js"></script>
</body>
</html>
```
CSS は `<head>〜</head>` 内で読み込み、JavaScript は `</body>` の直前などで読み込む必要がある。

**※** CDN で読み込むのが簡単だが、本番環境で CDN を使うかは検討する必要がある（バージョンアップにより CDN のアドレスが変更や廃止になる可能性がある）。

### 2.2. ファイルをダウンロードして、CSSとJSを適用させる方法

ローカルのファイルでやるか、クラウドのファイルでやるかだけの違いだけである。

### 2.3. NPMもしくはYarnで設定する方法

#### Yarnとは？

JavaScript(node.js)のパッケージマネージャで、2016年にFaceBookが公開したものである。

#### 設定方法

##### 1. 使いたいパッケージをインストール

`yarn add swiper`

##### 2. インストール

`yarn install`

必要なファイルが`node-module`ディレクトリ配下に作成される。

[![Image from Gyazo](https://i.gyazo.com/22d711c8dcdd8ef85d6bbb3d81433fee.png)](https://gyazo.com/22d711c8dcdd8ef85d6bbb3d81433fee)

#### 3. 導入したファイルの読み込み設定

(【Ver6以降】assets/javascript/application.js)
```
//= require swiper/swiper-bundle.js
//= require swiper.js

# この順番を間違えると上手く動かない
```

(【Ver６】assets/stylesheets/application.scss)
```
@import 'swiper/swiper-bundle';
```

(config/initializers/assets.rb)

```
Rails.application.config.assets.paths << Rails.root.join('node_modules')
```

#### 4. JSファイルの作成（先ほどのJSとは別！）

CDNから持ってくるJSファイル、もしくはYarnでインストールして`node_modules`配下に置かれるJSファイルとは別に、新しくJSファイルを自分で作成する必要があります。

このJSファイルによって、自分が適用したいオプションを設定することができる。

(app/assets/javascripts/swiper(任意の名前).js)
```
// var swiper = と始めるのではなく、$(function(){ で始める(jQueryでの設定)

$(function() {
    new Swiper('.swiper', {

        // Optional parameters
        direction: 'vertical',
        loop: true,

        pagination: {
            el: '.swiper-pagination',
        },

〜 以下省略 〜
```

#### 5. CSSの追加設定

(application.css)
```
.swiper {
    width: 600px;
    height: 300px;
}
```

# 参考

[RailsでSwiperを導入する方法（Swiperは2020年7月にバージョンアップし、従来と設定方法が変わりました！）- qiita](https://qiita.com/miketa_webprgr/items/0a3845aeb5da2ed75f82)

[swiperをyarnで導入して、画像をスライダー形式にする！ - qiita](https://qiita.com/ken_ta_/items/bdf04d8ecab6a855e50f)

[スライダープラグイン Swiper の使い方](https://www.webdesignleaves.com/pr/plugins/swiper_js.html)

[Swiper関連リンク](https://tattered-hen-04a.notion.site/Swiper-cc28ff16211e4afdbb7b35198ed97310)

[[Rails]Swiperで画像スライド作成 - qitta](https://qiita.com/yummy888/items/8528c7542f85ae7bbc55)

[サンプル付き！簡単にスライドを作れるライブラリSwiper.js超解説（基礎編）](https://garigaricode.com/swiper/)