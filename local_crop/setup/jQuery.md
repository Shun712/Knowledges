# jQueryとは?
jQueryとは、**Javascriptのライブラリ**である。  
jQueryでは、Javascriptで書くコードをより簡単に、少ない量で書くことができる。
```javascript
// jQueryなしの場合
document.getElementById("title").innerHTML = "テスト"

// jQueryありの場合
$("#title").html("テスト");
```

# jQueryの導入手順

### 1. yarnコマンドでjQueryをインストール

`yarn add jquery`

### 2. Webpackの設定

Webpackの設定ファイルでjQueryを管理下として認定する。

(config/webpack/environment.js)
```javascript
const { environment } = require('@rails/webpacker')
// 以下追記
const webpack = require('webpack')
environment.plugins.prepend('Provide',
    new webpack.ProvidePlugin({
        $: 'jquery/src/jquery',
        jQuery: 'jquery/src/jquery'
    })
)
// ここまで
module.exports = environment
```

### 3. application.jsの設定
`application.js`でjQueryを呼び出せるようにする。  
(javascript/packs/application.js)
```javascript
import Rails from "@rails/ujs"
import * as ActiveStorage from "@rails/activestorage"
import "channels"

require("jquery")

Rails.start()
ActiveStorage.start()
```

### 4. 動作確認
`app/javascript`フォルダに、`test.js`ファイルを作成し、コードを書く。
```javascript
$(function(){
    $("#test").css("color","red")
    $(".hoge").css("color","#00ff7f")
});
```
- 「#test」は、idが「test」のコードを指定

- `css("color", "red")`で、「色を赤にする」とする

- 「.hoge」は、classが「hoge」のコードを指定

- `css("color", "#00ff7f")`で、「色を、色コードが`#00ff7f`の色にする」とする

```html
<!DOCTYPE html>
<html>
  <head>
    <title>IbsDiary</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <%= yield %>
    <p id="test">jQueryです</p>
    <p class="hoge">色を変えます</p>
  </body>
</html>
```

###  5. jQueryが反応しない場合

[S]CSSやJavaScriptファイルのオートリロードする。

`./bin/webpack-dev-server`

# 参考

[Rails6でのjQuery導入方法 - qiita](https://qiita.com/tatsuhiko-nakayama/items/b2f0c77e794ca8c9bd74)

[Rails 6+Webpacker開発環境をJS強者ががっつりセットアップしてみた（翻訳）- TechRacho](https://techracho.bpsinc.jp/hachi8833/2021_05_06/83678)

[【Rails6】5分でjQueryを導入！　動作確認まで徹底](https://ymiyashitablog.com/rails-jquery/)

[【初心者向け】jQueryとは｜メリット・デメリットから記述方法まで解説](https://www.pasonatech.co.jp/workstyle/column/detail.html?p=2570)