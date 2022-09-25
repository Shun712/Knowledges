# エラー解消方法

- エラー分でググる

- 原因を細分化し、影響範囲を狭めていく。

[![Image from Gyazo](https://i.gyazo.com/2b8cd61607f2b6ac165289620acb23f9.png)](https://gyazo.com/2b8cd61607f2b6ac165289620acb23f9)

# Debuggerを使ったデバッグ方法

- 停止したい行で`debugger`を記載する。

- いちいち止まるのが嫌だなと思う場合は、`ブレークポイントをマーク`して実行する。

- 再生ボタンを押すと、Reactのコード自体がどのような順序で実行されているかわかる。

- escキーでコンソールが開く

[![Image from Gyazo](https://i.gyazo.com/40e8a72d15db278b3d97838e232d866b.png)](https://gyazo.com/40e8a72d15db278b3d97838e232d866b)

# React Developer Toolsを使う

- 開発用のbuildコードでなきゃデバッグできない。

- `component`タグをクリックするとReactのツリー構造が確認でき、引数(propsなど)の中身を見られる。

- `profiler`タグでは、録画ボタンを押してブラウザ操作すると、再レンダリングされた回数など確認できる。

# google検索の使い方

- `*`ワイルドカードを含めると任意となる。

- `-`をつけるとそれ以外の単語となる。

- `after:2021`とすると2021年以降の記事がヒットする。