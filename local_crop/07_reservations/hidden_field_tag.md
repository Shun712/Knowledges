# hidden_field_tag

`form_with`や`form_for`を利用して、ユーザーに何かを打ち込んでもらい時や、送信してもらいたい時に便利なメソッドである。

`hidden_field`、`hidden_field_tag`は用途が似ているが使い方が異なる。

### hidden_field

`form_for`や`form_with`内で使用する。

`= f.hidden_field :shampoo_id, value: shampoo.id`

第一引数にパラメータ名(シンボル)、第二引数部分にvalueとして受け渡す必要がある。

### hidden_field_tag

`hidden_field_tag`だけでも使用でき`単体でパラメーターを渡せる`。

`<%= hidden_field_tag :email, @user.email %>`

`hidden_field_tag` どのようなシンボルに(第一引数)、どの値を渡すか(第二引数)

# 参考

[f.hidden_fieldとhidden_field_tagの使い方【Ruby on Rails】](https://sakurawi.hateblo.jp/entry/hidden_field)

[[Rails]hidden_fieldとhidden_field_tagの違いについて！[初心者] - qiita](https://qiita.com/jackie0922youhei/items/6c4ba67db446e0c91944)