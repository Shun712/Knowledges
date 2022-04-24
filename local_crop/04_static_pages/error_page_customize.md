# エラーページを静的ページで作成

デフォルトだと以下のように味気ないエラーページとなっており不親切な印象がある。  
ユーザーにもわかりやすいように実装してみる。

[![Image from Gyazo](https://i.gyazo.com/6b90924f27a678f905c767a8c9888192.png)](https://gyazo.com/6b90924f27a678f905c767a8c9888192)

# 設定

開発環境で本番環境と同じエラーページを表示させるよう設定する。  
実装が終わったら、`true`に戻すのを忘れずに！！
```ruby
# config/environments/development.rb

config.consider_all_requests_local = false
```

# エラーページを修正

### 1. エラーページには以下の違い

- 404 Not Found: リソースが見つからなかった場合。
- 422 Unprocessable Entity: WebDAVの拡張ステータスコード。
- 500 Internal Server Error: サーバ内部でエラーが発生した場合に返される。

### 2. エラーページを修正

エラーページは拡張子が`.html`なので静的ページであるので、cssファイルの読み込み等はできない。  
cssなんかはhtmlファイルにベタ書きすれば見た目が変わる。  
画像を挿入したいときは、`public/images`に入れて
`<img src="https://hogehoge.com/images/[画像ファイル名]">`で表示させる。

```html
# public/404.html

<!DOCTYPE html>
<html>
<head>
  <title>The page you were looking for doesn't exist (404)</title>
  <meta name="viewport" content="width=device-width,initial-scale=1" charset="utf-8">
  <style>
    @media (min-width: 768px) {
      .container-md, .container-sm, .container {
        max-width: 100%;
      }
    }

    .py-5 {
      padding-top: 3rem !important;
      padding-bottom: 3rem !important;
    }

    .mb-lg-3 {
      margin-bottom: 1rem !important;
    }

    .row {
      --bs-gutter-x: 1.875rem;
      --bs-gutter-y: 0;
      display: flex;
      flex-wrap: wrap;
      margin-top: calc(-1 * var(--bs-gutter-y));
      margin-right: calc(-0.5 * var(--bs-gutter-x));
      margin-left: calc(-0.5 * var(--bs-gutter-x));
    }
    .row > * {
      flex-shrink: 0;
      width: 100%;
      max-width: 100%;
      padding-right: calc(var(--bs-gutter-x) * 0.5);
      padding-left: calc(var(--bs-gutter-x) * 0.5);
      margin-top: var(--bs-gutter-y);
    }

    .justify-content-center {
      justify-content: center !important;
    }

    .pt-lg-4 {
      padding-top: 1.5rem !important;
    }

    .text-center {
      text-align: center !important;
    }

    .col-lg-5 {
      flex: 0 0 auto;
      width: 41.66666667%;
    }

    .col-md-7 {
      flex: 0 0 auto;
      width: 58.33333333%;
    }

    .col-sm-9 {
      flex: 0 0 auto;
      width: 75%;
    }

    .display-404 {
      color: #fff;
      text-shadow: -0.0625rem 0 #fe696a, 0 0.0625rem #fe696a, 0.0625rem 0 #fe696a, 0 -0.0625rem #fe696a;
    }

    .display-404 {
      font-size: calc(2.125rem + 10.5vw);
      font-weight: 500;
      line-height: 1;
    }
    @media (min-width: 1200px) {
      .display-404 {
        font-size: 10rem;
      }
    }

    h6, .h6, h5, .h5, h4, .h4, h3, .h3, h2, .h2, h1, .h1 {
      margin-top: 0;
      margin-bottom: 0.75rem;
      font-weight: 500;
      line-height: 1.2;
      color: #373f50;
    }

    .mb-4 {
      margin-bottom: 1.5rem !important;
    }

  </style>
</head>

<body class="rails-default-error-page">
  <!-- This file lives in public/404.html -->
  <div class="container py-5 mb-lg-3">
    <div class="row justify-content-center pt-lg-4 text-center">
      <div class="col-lg-5 col-md-7 col-sm-9">
        <h1 class="display-404 py-lg-3">404</h1>
        <h2 class="h3 mb-4">ご指定のページが見つかりませんでした</h2>
      </div>
    </div>
  </div>
</body>
</html>

```


# 参考

[[Rails]404/500などのエラーページって結局どうすればいいの？](https://cpx.business/articles/how-to-create-an-error-page/)