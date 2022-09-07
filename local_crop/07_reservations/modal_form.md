# モーダルフォーム

前提としてbootstrap、jQueryを導入しておく。

# Ajax化

リンクに属性を追加。  
rails6による**バージョン違い**に注意！

```ruby
# index.html.erb

<%= link_to 'New User', new_user_path, remote: true, class: "btn btn-lg, btn-primary" %>
```

# new.js.erbの作成

`index.html.erb`の`id="user-modal"`の`<div>`タグに対して、新規作成用formレンダリング・表示する。

```ruby
# new.js.erb

$("#user-modal").html("<%= escape_javascript(render 'form') %>")
$("#user-modal").modal("show")
```

# _form.html.erbの編集

Bootstrapを用いて、`_form.html.erb`をmodal formとして表示させるため、`<div>`タグで囲む。

```html
<div class="modal-dialog" role="document">
  <div class="modal-content">
    <%= form_with(model: @user, local: true) do |form| %>
    <% if @user.errors.any? %>
    <div id="error_explanation">
      <h2><%= pluralize(@user.errors.count, "error") %> prohibited this user from being saved:</h2>
      <ul>
        <% @user.errors.full_messages.each do |message| %>
        <li><%= message %></li>
        <% end %>
      </ul>
    </div>
    <% end %>
    <div class="modal-header">
      <h5 class="modal-title">New User</h5>
      <button type="button" class="close" data-dismiss="modal" aria-label="Close">
        <span aria-hidden="true">&times;</span>
      </button>
    </div>
    <div class="modal-body">

      <div class="form-group field">
        <%= form.label :name , class: "form-control-label"%>
        <%= form.text_field :name, class: "form-control" %>
      </div>
    </div>
    <div class="modal-footer actions">
      <%= form.submit class: "btn btn-primary"%>
    </div>

    <% end %>
  </div>
</div>
```

[![Image from Gyazo](https://i.gyazo.com/57d8d5dba0ca1125fc6d40e376f595be.png)](https://gyazo.com/57d8d5dba0ca1125fc6d40e376f595be)

# 参考

[Rails Bootstrap with Modal Form - qiita](https://qiita.com/tsunemiso/items/edbc58becf55875c4fdb)