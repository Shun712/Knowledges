# yarnとは?

代表的なnode.jsのパッケージマネージャである。
nodeをインストールすると自動でインストールされるnpmと役割は同様である。
npmよりインストールが速い。

# Yarnを使ってbootstrap material designを導入する

**1. yarnのインストール**

`sudo npm install -g yarn`

**2. package.jsonの生成**

`package.json`でパッケージを一括管理できる。
プロジェクトにまだ`package.json`がない場合、以下のコマンドで生成できる。

`yarn init`

**3. yarnでパッケージをインストール**

`package.json`に記載されたモジュールをインストールする。

`yarn`

**4. パッケージの追加**

以下のコマンドでパッケージのインストールと`package.json`への追加ができる。

`yarn add bootstrap bootstrap-material-design jquery popper.js`

※ 必要なパッケージは

- Bootstrap本体の `bootstrap`

- `Material Design for Bootstrapのbootstrap-material-design`

- Bootstrapに必要な `jquery`

- Bootstrapに必要な `popper.js`

以上4つである。

※ パッケージのアンインストール

`yarn remove`

**5. マニフェストファイルへ読み込みのpathを記載**

(app/assets/javascripts/application.js)

```
// application.js

//= require jquery3
//= require popper
//= require bootstrap-material-design/dist/js/bootstrap-material-design.js
```

(app/assets/stylesheets/application.scss)

```
@import 'bootstrap-material-design/dist/css/bootstrap-material-design';
```

**6. application.erb.htmlの記述**

`app/views/layouts/application.erb.html`で

`<%= stylesheet_pack_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>`

へ変更する。

`stylesheet_link_tag`を`stylesheet_pack_tag`に変更している。

**7. jQueryとPopper.jsの有効化**

(app/config/webpack/environment.js)

```
const { environment } = require('@rails/webpacker') 
const webpack = require('webpack') 
 environment.plugins.append('Provide', 
   new webpack.ProvidePlugin({ 
     $: 'jquery', 
     jQuery: 'jquery', 
     Popper: ['popper.js', 'default'] 
   }) 
 ) 

 module.exports = environment
```

# 参考

[yarnとは - qiita](https://qiita.com/akitxxx/items/c97ff951ca31298f3f24)

[[Rails6.0] Rails6 + yarn + webpacker でMaterial Design for Bootstrapを導入する - qiita](https://qiita.com/sasakura_870/items/38e17d95d9497cf81413)

[【Rails】 font-awesome-sassの使い方を徹底解説！ - pikawaka](https://pikawaka.com/rails/font_awesome_sass)
