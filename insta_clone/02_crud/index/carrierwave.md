# CarrierWaveとは?

ファイルのアップロード機能を簡単に追加する事が出来るgemである。

CarrierWaveは、アップロードしたファイルの保存先はデフォルトで`public/uploads`だが、外部ストレージ(Amazon S3)にも設定できる。

# 導入手順

**1. Gemfileにcarrierwave追加**

`gem 'carrierwave', '~> 2.0'`

`bundle install`

**2. アップローダークラスの作成**

Carrierwaveをインストールすると、アップローダークラスを以下のコマンドで生成する事ができる。

`bundle exec rails g uploader Avatar`

コマンドを実行すると、ユーザーのアバター画像用のアップローダークラスを作成するファイル(app/uploaders/avatar_uploader.rb)が作成される。

[![Image from Gyazo](https://i.gyazo.com/577289475a690b89863eaba8bc6a92d5.png)](https://gyazo.com/577289475a690b89863eaba8bc6a92d5)

アップローダークラス(AvatarUploader)では、アップロードするファイルの拡張子やサイズ、保存するパスを指定する事ができる。

デフォルトで`storage :file`が指定されているので、アップロードしたファイルは`public/配下`に保存される。保存されるディレクトリは、`store_dir`メソッドで設定される。

**3. アップロード画像のカラムを追加**

`bundle exec rails g migration add_avatar_to_users avatar:string`

avatarカラムには、以下のように **「画像のデータ」ではなく「画像のファイル名」を保存される**。なぜなら、データベースの容量が圧迫されるからである。画像を表示するときに「画像が格納されているパス」と「DBに保存されているファイル名」を使う。

[![Image from Gyazo](https://i.gyazo.com/98496ecd1eeb9a39ab3d4f37003ebca7.png)](https://gyazo.com/98496ecd1eeb9a39ab3d4f37003ebca7)

データベースに保存できるように`users_controller`の`user_params`に`avatar`カラムを追加する。

```
def user_params
  params.require(:user).permit(:nickname, :age, :avatar) # 変更後
end
```

**4. アップローダークラスとカラムの紐付け**

ユーザーのアバター画像のアップロード機能を追加するので、Userモデルに先ほど作成したアバター画像用の「avatarカラム」と「AvatarUploaderクラス」を紐づけする。

```
class User < ActiveRecord::Base
  mount_uploader :avatar, AvatarUploader
end
```
これでアバター画像をアップロードする際に、`AvatarUploader`クラスの設定を利用できるようになる。

**5. アバター画像の登録・更新**

既存のフォームに`file_filed`でファイル選択ボックスを作成する。

```
<div class="field">
  <%= form.label :avatar %>
  <%= form.file_field :avatar %>
</div>
```

paramsには、フォームから送信された全ての情報が格納される。その中の`avatar`に、今回アップロードしたファイルの情報が入る。

[![Image from Gyazo](https://i.gyazo.com/910396eeef9a45920d9f47193b2f41f3.png)](https://gyazo.com/910396eeef9a45920d9f47193b2f41f3)

`@original_filename`は、アップロードしたファイルの名前(120185.png)で、この値がデータベースに保存される。

**6. アバター画像の表示**

アバター画像を表示させるには、まずは画像が保存されている場所(パス)を取得する必要がある。

Userモデルに、`AvatarUploader`クラスと`avatar`カラムを紐づけたので、以下の`AvatarUploader`クラスのメソッドを使って簡単にアップロードしたファイルの情報を取得することができる。

[![Image from Gyazo](https://i.gyazo.com/631b1dc18ffc217631375e3bfecca096.png)](https://gyazo.com/631b1dc18ffc217631375e3bfecca096)

```
irb(main):001:0> user = User.first
  User Load (0.6ms)  SELECT  `users`.* FROM `users` ORDER BY `users`.`id` ASC LIMIT 1
=> #<User id: 1, nickname: "ピカ子", age: 18, created_at: "2020-02-25 13:21:31", updated_at: "2020-02-25 13:43:54", avatar: "120185.png">

irb(main):002:0> user.avatar.url
=> "/uploads/user/avatar/1/120185.png"

irb(main):003:0> user.avatar.current_path
=> "/Users/username/directory/sample_app/public/uploads/user/avatar/1/120185.png"

irb(main):004:0> user.avatar_identifier
=> "120185.png"
```

```
<% if @user.avatar? %>  <!-- アップロード画像がある場合に実行する -->
  <p>
    <strong>Avatar:</strong>
    <%= image_tag @user.avatar.url %><!-- userインスタンスの画像ファイルのURLを取得し表示 -->
  </p>
<% end %>
```

# アップロードファイルをgit管理対象外に設定

**アップロードした画像は「public/uploads/モデル名/画像のカラム名/id」配下に保存されます**。

[![Image from Gyazo](https://i.gyazo.com/0adc5d72d56a803549f1dec7356e24d4.png)](https://gyazo.com/0adc5d72d56a803549f1dec7356e24d4)

まとめると、アップロード画像のファイル名はDBに保存され、実際の画像は`public/uploads/モデル名/画像のカラム名/id`に保存される。

**画像は、`Github`などにアップロードする必要がないので`.gitignore`に`/public/uploads`を指定してGit管理下から除外する。**

# 複数画像の場合

`bundle exec rails g migration add_avatars_to_users pictures:json`

(models/user.rb)
```
class User < ApplicationRecord
 # mount_puloadersと複数形になる
 mount_uploaders :avatars, AvatarUploader
 # 複数の画像を取り扱う場合、serializeメソッドが必要
 serialize :avatars, JSON
end
```
(views/users/new.html.erb)
```
<%= form_with(model: User.new, multipart: true, local: true) do |form| %>
 <%= form.file_field :avatars, multiple: true %>
<% end %>
```
(controllers/users_controller.rb)
```
def user_params
 params.require(:user).permit(..., {avatars: []})
end
```
(views/users/show.html.erb)
```
<% @user.avatars.each do |avatar| %>
 <%= image_tag(avatar.url, size: "30x30") unless avatar.file.nil? %>
<% end %>
```

# 参考
[【Rails】 CarrierWaveチュートリアル - pikawaka](https://pikawaka.com/rails/carrierwave)

[画像周りの扱い方 - qiita](https://qiita.com/joaoki0412/items/64cb44592923bde2e8ff)

[Github: carrierwaveuploader/carrierwave](https://github.com/carrierwaveuploader/carrierwave)

