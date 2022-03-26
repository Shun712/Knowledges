# npm(Node Package Manager)とは

Node.jsのパッケージを管理するシステム
rubygems.orgと似ている。

# パッケージとは?

- モジュールをまとめて機能するようにしたもの。  
- npmでダウンロードして使用するものがパッケージである。

# npmの必要性

- rubyのbundlerと同じように、パッケージ同士で依存関係や競合関係があるので、npmの管理が必要となる。
- yarnも同じような特徴があるが、npmよりインストールが早い。

# Node.js管理ツール

- nvm、nodebrew、nodenvなどというNode.jsのバージョン管理システムで管理する
- Node.jsはバージョンアップが頻繁に行われているので、できるだけnvmなどで管理するようにする。

# package.jsonとは

プロジェクトの構成、構造を示した設計書のようなもの。

# 参考

[そもそもnpmからわからない](https://zenn.dev/antez/articles/a9d9d12178b7b2)

[Node.js管理ツールの更新頻度とスター数を比較してみた - qiita](https://qiita.com/tora_oba/items/8f8b7d3e5fb62bc96a3f)