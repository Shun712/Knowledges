# 14 SEO対策 メタタグの設定

# やったこと
- SEO対策として必須であるメタタグの設定
- gem 'meta-tags'で実装

# SEOとは?

「検索エンジン最適化（Search Engine Optimization）」の略称で、Googleなどの検索エンジンで検索された際に、上位に表示されやすくすることである。  
日本における主要な検索エンジンは、Googleが90％以上なので**「SEO対策 = Google対策」**である。

# SEOの目的

SEOの目的は、ホームページの検索ランキングの向上だけではない。  
検索から流入したユーザーがどんな目的でサイトを閲覧しているか(検索意図)
を読み取り、ユーザーニーズを満たすコンテンツの作成や目的ページへ遷移しやすい
構成、ナビゲーション配置など、緻密にサイトを設計する必要がある。

# OGPとは?

「Open Graph Protocol」の略称で、FacebookやTwitterなどSNSでシェアした際に、
設定したWEBページのタイトルやイメージ画像、詳細などを伝えるHTML要素である。

# Metaタグの反映

[![Image from Gyazo](https://i.gyazo.com/92f219c5046b297fa6ee08216eb61235.png)](https://gyazo.com/92f219c5046b297fa6ee08216eb61235)

# gem 'meta-tags'とは?

> Ruby on Railsアプリケーション用の検索エンジン最適化（SEO）プラグイン。
> Google翻訳
> [meta-tags - github](https://github.com/kpumuk/meta-tags)

主に内部的対策として、`title`, `desciption` の設定をする。  

> [gem 'meta-tags'とは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/14_metatag/index/gem_meta-tags.md)

# ngrokとは?

ngrokは「エングロック」と発音し、トンネリングを用いて
ローカルPCのWebサーバーを外部公開できるツールである。

> [ngrokとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/14_metatag/index/ngrok.md)

# 学んだこと

リンクを貼った際にページの詳細が表示される仕組みが理解できた。  
SEO対策はかつて聞いたことがあったが、設定をしなければおそらく一生検索されないだろうと思う。 
実務でも必ず必要な実装であると思うので理解を深めていきたい。
