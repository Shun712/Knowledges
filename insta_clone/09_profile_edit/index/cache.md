# cache(キャッシュ)とは？

バリテーションの失敗後でも、アップロードしたファイルを記憶・保持してくれる機能のことである。

# 実装

- 画像アップロード時に、「(カラム名)_cache」の`hidden_field`を追加する

- ストロングパラメータに、「(カラム名)_cache」を記述する

```html
= form_with model: @user, url: mypage_account_path, method: :patch, local: true do |f|
  = render 'shared/error_messages', object: f.object
  .form-group
    = f.label :avatar
    = f.file_field :avatar, onchange: 'previewFileWithId(preview)', class: 'form-control', accept: 'image/*'
    = f.hidden_field :avatar_cache
```

このように記述すると、`hidden_field`の中に画像データが保存され、バリテーションに引っ掛かった後でも、データを引き継げる。  
これにより、画像をもう一度入力せずに、ユーザー名を入力するだけで更新できる。


[![Image from Gyazo](https://i.gyazo.com/05c40e04e4387a1f96f47463c540fd9d.png)](https://gyazo.com/05c40e04e4387a1f96f47463c540fd9d)

# 参考

[hidden_fieldの使い方 - qiita](https://qiita.com/yukiweaver/items/8e1e01fd6dcadf36d420)

[【Rails】CarrierwaveのCache機能を使用し、バリデーション後の画像データを保持する方法](https://techtechmedia.com/cache-carrierwave-rails/)