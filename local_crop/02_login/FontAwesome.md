# Font Awesomeの導入

### 1. インストール

`yarn add @fortawesome/fontawesome-free`

### 2. Font Awesomeを読み込ませる

(app/javascript/packs/application.js)
```javascript
import 'bootstrap';
import '@fortawesome/fontawesome-free/js/all'; //追加
import '../stylesheets/application';
```

(app/javascript/stylesheets/application.scss)
```scss
@import '~bootstrap/scss/bootstrap';
@import '~@fortawesome/fontawesome-free/scss/fontawesome'; //追加
```

# 参考

[【図解あり】Rails6でFont Awesomeを用いてSNSアイコンを表示させる - qiita](https://qiita.com/mitaninjin/items/25f5d65fe99f9fc529da)