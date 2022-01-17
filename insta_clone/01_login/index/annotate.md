# annotateとは？

各モデルのスキーマ情報をファイルの先頭もしくは末尾にコメントとして書き出してくれるGem。
カラム情報やルーティングを確認する手間が省くことができる。

# 導入方法

1. 準備

Gemfileに以下を記述して、インストール。

`gem 'annotate'`

`$ bundle install`

2. 設定ファイルを作成

`$ bundle exec rails g annotate:install`

このコマンドを実行すると、`lib/tasks/auto_annotate_models.rake`が作成される。
このファイルで設定を色々変えられる。

下記のように、自動的にファイルの先頭にスキーマ情報が書き出される。
```
# == Schema Information 
#
# Table name: users
#
#  id         :integer          not null, primary key
#  age        :integer
#  email      :string
#  name       :string
#  created_at :datetime         not null
#  updated_at :datetime         not null
#

class User < ApplicationRecord
end
```

### 参考

[【Rails】annotateの使い方](https://qiita.com/koki_develop/items/ae6b5f41c18b2872d527)
