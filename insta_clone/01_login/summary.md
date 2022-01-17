# 01 ログイン機能の実装

## Railsの環境構築
> [【完全版】MacでRails環境構築する手順の全て](https://qiita.com/kodai_0122/items/56168eaec28eb7b1b93b)
> [最速！MacでRuby on Rails環境構築](https://qiita.com/narikei/items/cd029911597cdc71c516)

## git-flowとは
プラグイン(ツール)のことである。それぞれの役割を持った、5つのブランチで管理する。
**開発者の流れ**
1. featureブランチを切ってコツコツ開発する。
2. プルリクを送り、レビューを受けてdevelopブランチへマージする。
3. featureブランチを削除する
4. リリースする準備が整ったら、releaseブランチを作成しデプロイして問題ないか確認する。
5. 問題があれば修正し、developブランチへマージする。問題がなければ、masterブランチへマージする。
[![Image from Gyazo](https://i.gyazo.com/6d6d7e51a54c23d65d7b921bccba5eaa.png)](https://gyazo.com/6d6d7e51a54c23d65d7b921bccba5eaa)

> [git-flowとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/01_login/index/git-flow.md)

## turbolinkとは
Rails4から正式導入された画面遷移を高速化させるライブラリである。
Railsではデフォルトでgemとして組み込まれている。
> [turbolinksとは？](https://github.com/Shun712/Knowledges/blob/master/insta_clone/01_login/index/turbolinks.md)

## slimとは
slimはRubyで使うテンプレートエンジンの一つ。
slimには閉じタグが存在しないのでコード自体が非常にスッキリしている。
> [slimとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/01_login/index/slim.md)

## sorceryとは
> sorceryとは、Railsに認証機能の実装を行うためのライブラリです。 同じように認証機能を提供してくれているものとしてdeviseなどが挙げられますが、sorceryの方がよりシンプルで、カスタマイズ性に富んでいるという特徴を持ちます。
 
引用[【Rails】sorceryについて](https://boku-boc.hatenablog.com/entry/2020/10/10/213625)
> [sorceryとは？](https://github.com/Shun712/Knowledges/blob/master/insta_clone/01_login/index/sorcery.md)

## rubocopとは
Rubyの静的コード解析を実行するgemであり、インデントやメソッド名、改行などのチェックをしてくれるものである。
開発を進めていくと、rubocop機能は忘れがちになるので注意が必要である。
[【Ruby on Rails】rubocop と pre-commit を利用して git commit 時にコーディングチェックを行う](https://techblog.kyamanak.com/entry/2018/06/19/221910)

> [rubocopとは？](https://github.com/Shun712/Knowledges/blob/master/insta_clone/01_login/index/rubocop.md)

## redisとは

NoSQLの中でも、KVS(キーバリューストア)。キーとバリューの組み合わせを保存する。
Redisのデータはすべてメモリ内に保存されるため、高速なデータの読み書きが可能である。
また、セッションデータの場合は、Redisへ変更することでセッションハイジャックなどのセキュリティリスクを軽減できる。
[![Image from Gyazo](https://i.gyazo.com/5cd7f4ed6a97708035eb48f9ecdf8cb6.png)](https://gyazo.com/5cd7f4ed6a97708035eb48f9ecdf8cb6)

> [redisとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/01_login/index/redis.md)

## annotateとは
各モデルのスキーマ情報をファイルの先頭もしくは末尾にコメントとして書き出してくれるGem。
カラム情報やルーティングを確認する手間が省くことができる。
> [annotateとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/01_login/index/annotate.md)

## i18nとは
> アプリケーションの文言を英語以外の別の1つの言語に翻訳する機能や多言語サポート機能を簡単かつ拡張可能な方式で導入するためのフレームワークを提供
> [Rails 国際化 (i18n) API - Railsガイド](https://railsguides.jp/i18n.html)
 
Internationalizationの略で、"I"と"n"の間に18文字あるので、`I18n`となる。

細かい設定方法は、以下細かい設定方法は、[[初学者]Railsのi18nによる日本語化対応 - qiita](https://qiita.com/shimadama/items/7e5c3d75c9a9f51abdd5)を参照。

> [i18nとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/01_login/index/i18n.md)

## database.ymlとは
Railsにおけるデータベースの設定ファイルである。Railsアプリケーションを作成すると自動的に生成され、デフォルトではSQLiteを使用する前提で作成されるので、アプリケーションを作成する際に明示的にオプションでデータベースを指定する必要がある。

> [database.ymlとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/01_login/index/database.yml.md)

## migrationファイルとは
DBのテーブルに変更を加える際に、マイグレーションファイルを実行する。
マイグレーションファイルを実行することで、記述した内容に基づいたデータテーブルが生成される。

## schema.rbとは
データベースの構造を示すもの。
マイグレーションファイルを実行すると、データベースの構造が変わる。

## config/application.rbとは
`rails g`すると色々なファイルが自動生成されるが、不要なファイルも一緒に生成されるので、
`config/application.rb`に設定することで、ファイル生成を制限できる。

> [ファイル生成を制限](https://github.com/Shun712/Knowledges/blob/master/insta_clone/01_login/index/application.rb.md)

## yarnとは
代表的なnode.jsのパッケージマネージャである。
nodeをインストールすると自動でインストールされるnpmと役割は同様である。
npmよりインストールが速い。

> [yarnとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/01_login/index/yarm.md)