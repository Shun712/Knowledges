# 日付、時間入力のヘルパーメソッド

`xxxx_select`と、`xxxx_field`と２種類用意されている。

## xxxx_select

### data_select

[![Image from Gyazo](https://i.gyazo.com/888bff34ff21c58701ecccb8589417c3.png)](https://gyazo.com/888bff34ff21c58701ecccb8589417c3)

```ruby
.form-group
= f.label :created_at, class: 'control-label'
= f.date_select :created_at, class: 'form-control'
```

### datetime_select

[![Image from Gyazo](https://i.gyazo.com/96573ea9d4a9e3ae22ea471cd4124dbd.png)](https://gyazo.com/96573ea9d4a9e3ae22ea471cd4124dbd)

```ruby
.form-group
  = f.label :created_at, class: 'control-label'
  = f.datetime_select :created_at, class: 'form-control'
```

## xxxx_field

### date_field

[![Image from Gyazo](https://i.gyazo.com/346caad8d9f38ed32c1e96a9f471ced4.png)](https://gyazo.com/346caad8d9f38ed32c1e96a9f471ced4)

```ruby
.form-group
  = f.label :created_at, class: 'control-label'
  = f.date_field :created_at, class: 'form-control'
```

### datetime_field

[![Image from Gyazo](https://i.gyazo.com/7d08229d9f638ca4bd2787bff8b7378a.png)](https://gyazo.com/7d08229d9f638ca4bd2787bff8b7378a)

```ruby
.form-group
  = f.label :created_at, class: 'control-label'
  = f.datetime_field :created_at, class: 'form-control'
```

# 参考

[Rails 日付、時間入力のヘルパーメソッド ６種類 - qiita](https://qiita.com/pyon_kiti_jp/items/747496d02bdb1eff1ce8)