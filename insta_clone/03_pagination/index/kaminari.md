# kaminariとは?

rubyのgemの一つでページネーションを簡単に実装するためのもの。

# なぜページネーションの必要性

例えば、投稿一覧がトップページに表示されるサイトの場合、全ての投稿がトップページに表示されると読み込むまでに時間がかかりる上に、かなり読みにくくなる。

また、Railsのパフォーマンスも低下してしまう。

# 実装手順

#### 1. gemをインストール

`gem 'kaminari'`

`bundle install`

#### 2. kaminariの設定ファイルを作成

`rails g kaminari:views bootstrap4`

このコマンドによって、bootstrapなどのcssのフレームワークを取り入れたビューファイル(slimで実装していたらslim形式で)が自動で作成される。

> [Github:kaminari(#for-hamlslim-users)](https://github.com/kaminari/kaminari#general-configuration-options)
> [Github:kaminari(#themes)](https://github.com/kaminari/kaminari#general-configuration-options)

※ `rails g kaminari:config`を実行して`config/initializers/kaminari_config.rb`に表示件数など設定もできる。

> [Github:kaminari(#general-configuration-options)](https://github.com/kaminari/kaminari#general-configuration-options)

#### 3.ページネーションを定義

コントローラは下記を定義
```
def index
  @posts = Post.all.includes(:user).order(created_at: :desc).page(params[:page]).per(10)
end
```
ビューファイルは下記を定義
```
<%= paginate @posts %>
```

#### 4. kaminariを日本語化する

ビューファイルではページネーション内の文字を変更することはできない。
デフォルトだと英語なので日本語にしたい時は新たなファイルを作成する。

`config/locales`フォルダに`kaminari_ja.yml`というファイルを作成し、下記を書く。

```
ja:
  views:
    pagination:
      first: "&laquo; 最初"
      last: "最後 &raquo;"
      previous: "&lsaquo; 前"
      next: "次 &rsaquo;"
      truncate: "..."
  helpers:
    page_entries_info:
      one_page:
        display_entries:
          zero: ""
          one: "<strong>1-1</strong>/1件中"
          other: "<strong>1-%{count}</strong>/%{count}件中"
      more_pages:
        display_entries: "<strong>%{first}-%{last}</strong>/%{total}件中"
```

# 参考

[【Rails】 kaminariの使い方を理解してページネーションを実装しよう - pikawaka](https://pikawaka.com/rails/kaminari)

[Github:kaminari](https://github.com/kaminari/kaminari)