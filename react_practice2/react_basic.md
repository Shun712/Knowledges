# Reactの基礎

- `<script>`内の処理が`<div id="app"></div>`内に挿入される。

- `ReactDOM.render(<h1>こんにちは</h1>, appE1);`の書き方は現在非推奨になっている。

[![Image from Gyazo](https://i.gyazo.com/04cb7fc05e6545f06be9bfdeb893433b.png)](https://gyazo.com/04cb7fc05e6545f06be9bfdeb893433b)

# コンポーネント

画面の各構成要素をReactで定義したもの

- 再利用性、可読性、疎結合

[![Image from Gyazo](https://i.gyazo.com/120e4a5d0a36f0d956b05c2bd68f5d94.png)](https://gyazo.com/120e4a5d0a36f0d956b05c2bd68f5d94)

- コンポーネントの先頭は大文字なので、関数の先頭も**大文字**にする。

- `return`後が複数にまたがる場合、`return ()`とする。

[![Image from Gyazo](https://i.gyazo.com/d310e8fbe4c8c60d1313c58a00a685c2.png)](https://gyazo.com/d310e8fbe4c8c60d1313c58a00a685c2)

# コンポーネントの分割方法

[![Image from Gyazo](https://i.gyazo.com/66da8f792f016452ef8ed12ccde5c89e.png)](https://gyazo.com/66da8f792f016452ef8ed12ccde5c89e)

以下はコンポーネントの中身

[![Image from Gyazo](https://i.gyazo.com/3b7f0ed3203c68c11bb9af202e17e5f3.png)](https://gyazo.com/3b7f0ed3203c68c11bb9af202e17e5f3)

以下はどちらでも可

```javascript
export const hoge = () => {};
```

```javascript
const hoge = () => {};

export { hoge };
```

# 不要なタグを必要としないフラグメント

- JSX内の`root要素`は1つだけにする必要がある。

- 今回は、`<div> <h3> <p>`と3つあるので、`<React.Fragment>`で囲うとタグの数はそのままになる。

- Fragmentに付けられる属性を`key`だけ。

- Fragmentのインポートの仕方は2通りある。

[![Image from Gyazo](https://i.gyazo.com/7c24ba11d8ce02db6241b6e2497ab82f.png)](https://gyazo.com/7c24ba11d8ce02db6241b6e2497ab82f)

# JSX内でJSを実行

[![Image from Gyazo](https://i.gyazo.com/1d91fd5958db2032d29e143867329592.png)](https://gyazo.com/1d91fd5958db2032d29e143867329592)

- JS、変数、配列をJSX内で実行できる。

- とりあえず波括弧で囲んで実行できる。

[![Image from Gyazo](https://i.gyazo.com/9a1fed9d9a18b4a5d47677e2ffdc67e5.png)](https://gyazo.com/9a1fed9d9a18b4a5d47677e2ffdc67e5)

- 文は式を代入できない。

- 文は`return`の中で書かなければOK

# propsでコンポーネントに値を渡す

- props経由で値を渡すのが一般的

[![Image from Gyazo](https://i.gyazo.com/524b67053ab742ce556d44a5e7d4865b.png)](https://gyazo.com/524b67053ab742ce556d44a5e7d4865b)

[![Image from Gyazo](https://i.gyazo.com/0dfa2c30f357bfbb47156c89fa7d0c89.png)](https://gyazo.com/0dfa2c30f357bfbb47156c89fa7d0c89)

# propsの様々な渡し方

- 配列は`obj={{ name: 'Tom', age: 18 }}`のように`{{ }}`二重波括弧で渡す。

- `const o`が配列だった場合、スプレッド演算子`{...o}`でコンポーネントに中身を渡せる。

[![Image from Gyazo](https://i.gyazo.com/acbff83f4b6def26904df390e0f0bb81.png)](https://gyazo.com/acbff83f4b6def26904df390e0f0bb81)

- propsが何も渡されていない場合、コンポーネントの引数に初期値を与られる。

- propsが渡されている場合は、その値が入る。

[![Image from Gyazo](https://i.gyazo.com/98ec7aa8dd9c0aef0d691d775400bfc8.png)](https://gyazo.com/98ec7aa8dd9c0aef0d691d775400bfc8)

- コンポーネントにpropsを配列で渡す場合、`key`は`unique`である必要がある。

[![Image from Gyazo](https://i.gyazo.com/444bfc7a3435f90f422bb03f1aa1a9bd.png)](https://gyazo.com/444bfc7a3435f90f422bb03f1aa1a9bd)

- コンポーネントを`{ }`でpropsを送ることもできる。

[![Image from Gyazo](https://i.gyazo.com/7ff54cac20fc89fe5280e688a13abdfc.png)](https://gyazo.com/7ff54cac20fc89fe5280e688a13abdfc)

- データは以下のように`props`として渡す。

[![Image from Gyazo](https://i.gyazo.com/affdbb3b7d2274d9407bad8bccc94348.png)](https://gyazo.com/affdbb3b7d2274d9407bad8bccc94348)

- JSXはJSオブジェクトに変換しないと扱えない！

- タグは`type`、props、childrenとなる。

[![Image from Gyazo](https://i.gyazo.com/65ec19c8dc7351936f1b7bb5d316129b.jpg)](https://gyazo.com/65ec19c8dc7351936f1b7bb5d316129b)

[![Image from Gyazo](https://i.gyazo.com/736d4549d7e1d741754260e006403548.png)](https://gyazo.com/736d4549d7e1d741754260e006403548)

[![Image from Gyazo](https://i.gyazo.com/e1ece7fcd189c2ff7ba8b573295b6353.png)](https://gyazo.com/e1ece7fcd189c2ff7ba8b573295b6353)