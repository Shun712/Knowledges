# gem 'meta-tags'とは?

> Ruby on Railsアプリケーション用の検索エンジン最適化（SEO）プラグイン。
> Google翻訳
> [meta-tags - github](https://github.com/kpumuk/meta-tags)

主に内部的対策として、`title`, `desciption` の設定をする。

# metaタグとは？

metaタグとは、設定することでサイト名やタイトル名などや、
OGP設定、Google検索に載せたくないページを設定することができる。

# 実装手順

#### 1. gemをインストール

`gem 'meta-tags'`

#### 2. 設定ファイルの作成

`$ bundle exec rails generate meta_tags:install`を実行して、  
`config/initializers/meta_tags.rb`を作成する。  

このファイルでは、「title文字数制限」「descriptionの文字数制限」などが設定できる。

#### 3. default_meta_tagsの用意

metaタグの初期設定をするため、`app/helpers/application_helper.rb`に  
`default_meta_tags`を実装する。

```ruby
module ApplicationHelper
  def default_meta_tags
    {
      site: Settings.meta.site,
      reverse: true,
      title: Settings.meta.title,
      description: Settings.meta.description,
      keywords: Settings.meta.keywords,
      canonical: request.original_url,
      og: {
        title: :full_title,
        type: Settings.meta.og.type,
        url: request.original_url,
        image: image_url(Settings.meta.og.image_path),
        site_name: :site,
        description: :description,
        locale: 'ja_JP'
      },
      twitter: {
        card: 'summary_large_image'
      },
    }
  end
end
```

#### 4. metaタグの出力

`app/views/layouts/application.html.slim`のhead内に以下を記述
```ruby
doctype html
html
  head
    meta content=("text/html; charset=UTF-8") http-equiv="Content-Type" /
    meta[name="viewport" content="width=device-width, initial-scale=1.0"]
    / metaタグの初期設定を行う
    = display_meta_tags(default_meta_tags)
    = csrf_meta_tags
    = csp_meta_tag
```

#### 5. 別ページでmetaタグの上書きを行う

ページごとにmetaタグを書き換えるために、記事ごとに上書きする。
(`app/views/posts/show.html.slim`)
```ruby
- set_meta_tags title: '投稿詳細ページ', description: @post.body,
        og:  { image: "#{request.base_url}#{@post.images.first.url}" } 
.post-detail.card
以下省略
```
 
# 参考

[meta-tags - github](https://github.com/kpumuk/meta-tags)

[【Rails】『meta-tags』gemを使ってSEO対策をおこなう方法](http://vdeep.net/rubyonrails-meta-tags-seo)

[【Rails】meta-tagsを使う - qiita](https://qiita.com/healing_code/items/731b7d80a0b080b3a86d)

[[Rails] metaタグを設定する方法 -qiita](https://qiita.com/momo1010/items/ccb507c013976846a549)

[Railsのrequestで取得できる情報の具体例をまとめた](https://l-light-note.hatenablog.com/entry/2018/04/26/140301)