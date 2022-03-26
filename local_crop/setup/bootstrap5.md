# bootstrap5の導入

bootstrap5から**jQuery**に依存しなくなった。

# 導入手順

### 1. bootstrap5のインストール

`yarn add bootstrap`

### 2. @popper.js/coreをインストール

アニメーション周りで必要なライブラリである。

`yarn add @popperjs/core`

### 3. ファイルの書き換え

`stylesheet_link_tag`から`stylesheet_pack_tag`へ書き換える。  

(app/views/layouts/application.html.slim)
```ruby
doctype html
html
  head
    title
      | LocalCrop
    meta[name="viewport" content="width=device-width,initial-scale=1"]
    = csrf_meta_tags
    = csp_meta_tag
    = stylesheet_pack_tag 'application', media: 'all'
    = javascript_pack_tag 'application'
  body
    = yield
```

### 4. CSS読み込み設定

`Webpack`でのCSSの読み込みのためのディレクトリとファイル(エントリポイント)を作成
```ruby
$ mkdir ./app/javascript/stylesheets
$ touch ./app/javascript/stylesheets/application.scss
```
作成したファイル内に以下を記述する。  
`@import "~bootstrap/scss/bootstrap.scss";`

最後に、`application.scss`を読み込ませる。
```ruby
import Rails from "@rails/ujs"
import * as ActiveStorage from "@rails/activestorage"
import "channels"
import "bootstrap";
import "../stylesheets/application.scss";

Rails.start()
ActiveStorage.start()
```