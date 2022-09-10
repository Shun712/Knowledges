# packageのインストール

`package.json`に記載されているライブラリを  
`$ npm install`  
でインストールできる。

すると、`node-module`のフォルダができる。

# アロー関数

### メリット

- 簡略化しているので、関数の記述が少なくなる。

- 関数の詳細が一行だと以下のようになる。

  - 引数が一つだと`()`は省略できる。

[![Image from Gyazo](https://i.gyazo.com/616135612e4988f8797b5a7a5885de83.png)](https://gyazo.com/616135612e4988f8797b5a7a5885de83)

# プロパティ

以下は`result`というプロパティに結果を返す。

[![Image from Gyazo](https://i.gyazo.com/4d4f6a23f9761c5abe806a8141a94e8a.png)](https://gyazo.com/4d4f6a23f9761c5abe806a8141a94e8a)

[![Image from Gyazo](https://i.gyazo.com/9ec5b506a1ab8996598b2e33ef15b119.png)](https://gyazo.com/9ec5b506a1ab8996598b2e33ef15b119)

# コールバック関数

コールバック関数とは、**引数に渡された**関数のこと。

→　`fn()` とは `関数(別の関数)`

[![Image from Gyazo](https://i.gyazo.com/82eb8077bfdbb27a715ced9df4a8a421.png)](https://gyazo.com/82eb8077bfdbb27a715ced9df4a8a421)

# debuggerを使う

コードの前に`debugger;`と書いて内容を調べられる。

# DOMとイベントリスナ

- DOMとはHTMLにあるタグ(`<div> <a> <body>`)などを扱う。  

- javascriptでは、これらのタグはDOMを介さないと扱えない。  

# documentでhtmlのタグを扱う

以下は、`h1Element`というオブジェクト(**DOMと呼ぶ**)に`document.querySelector('h1')`で取得。

[![Image from Gyazo](https://i.gyazo.com/172ba65740fedfb71f7e4cfb6611c745.png)](https://gyazo.com/172ba65740fedfb71f7e4cfb6611c745)

`console.dir(h1Element)`でDOMオブジェクトの実態を見られる。

[![Image from Gyazo](https://i.gyazo.com/694edb80ec321d18167303ed5f226ea2.png)](https://gyazo.com/694edb80ec321d18167303ed5f226ea2)

`h1Element.textContent = '変更後タイトル'`でHTMLのテキストを変更できる。

# e（イベントハンドラー）

ブラウザで「クリック」されたとき、`helloFn`というコールバック関数の引数`(e)`が`addEventListner`に渡される。

[![Image from Gyazo](https://i.gyazo.com/833dbfd6597209d188a410af0e00747e.png)](https://gyazo.com/833dbfd6597209d188a410af0e00747e)

以下は、`(e.target)`におけるDOMオブジェクトの実態である。

[![Image from Gyazo](https://i.gyazo.com/4721346c42049fa9cc5cbd7d79504d19.png)](https://gyazo.com/4721346c42049fa9cc5cbd7d79504d19)

# map、 filterメソッド

- mapメソッドでは、第一引数に`value`、第二引数に`index`、第三引数に`array`とその配列自身を指定できる。

- `return`で値を返さなければ、値が配列に格納されない。

- ここでは、`map`メソッド内の`val`がコールバック関数になる。

[![Image from Gyazo](https://i.gyazo.com/6799316a0f5cad070b3f026b5fb4a7d4.png)](https://gyazo.com/6799316a0f5cad070b3f026b5fb4a7d4)

# 分割代入

- 配列の場合、順番が関係する。

- オブジェクトの場合、プロパティ(`x:` とか　`z:`)名と一致させる。

[![Image from Gyazo](https://i.gyazo.com/3a6a9ae50dbb08a6cf3129f5dd5a1ffe.png)](https://gyazo.com/3a6a9ae50dbb08a6cf3129f5dd5a1ffe)

以下2つはどちらでも可！

[![Image from Gyazo](https://i.gyazo.com/9b355001c16c4f2859472373e5a8d03c.png)](https://gyazo.com/9b355001c16c4f2859472373e5a8d03c)

[![Image from Gyazo](https://i.gyazo.com/741a877918024e941d34dfa8fd89e50b.png)](https://gyazo.com/741a877918024e941d34dfa8fd89e50b)

[![Image from Gyazo](https://i.gyazo.com/9a21d28a8e202dfb0d075e26a5de2af7.png)](https://gyazo.com/9a21d28a8e202dfb0d075e26a5de2af7)

# スプレッド演算子

- 配列（もしくはオブジェクト）の要素が一つずつ展開されて、引数に渡される。

- 配列（もしくはオブジェクト）を代入したものとスプレッド演算子で代入したものは**false**になる。

[![Image from Gyazo](https://i.gyazo.com/d100fc495cd5fd3af86b93694373a3da.png)](https://gyazo.com/d100fc495cd5fd3af86b93694373a3da)

`...argA`の部分は残余演算子などと呼ぶ。

[![Image from Gyazo](https://i.gyazo.com/7624e82dbdfa9f04ddd2ad4d1676774c.png)](https://gyazo.com/7624e82dbdfa9f04ddd2ad4d1676774c)

# 三項演算子

- 1は`true`、 0は`false`を返す。

- 文字列の`"0"`は`true`を返す。

[![Image from Gyazo](https://i.gyazo.com/382f342c5090067f114f3c59f50579b5.png)](https://gyazo.com/382f342c5090067f114f3c59f50579b5)

# 非同期処理(Promise)

- Promiseには`resolve`と`reject`の関数を引数に取る。

- `resolve`は関数内で呼ばれると、`then`のコールバック関数が実行される。

- `reject`は関数内で呼ばれると、`catch`のコールバック関数が実行される。

- `then`は連続できるが、コールバック関数の引数が渡ってこないので直前のコールバック関数で返り値を渡してあげる。

[![Image from Gyazo](https://i.gyazo.com/63a114e7a10b9674bcf2f55ad95f8c24.png)](https://gyazo.com/63a114e7a10b9674bcf2f55ad95f8c24)

# 非同期処理(await/ async)

- `await`を用いた場合、先頭に`async`を記述しなければならない。

- `then`を使うよりシンプルに記述できる。

[![Image from Gyazo](https://i.gyazo.com/90918aad90dd14a971215a3198b44ae1.png)](https://gyazo.com/90918aad90dd14a971215a3198b44ae1)

## tryで例外処理

- `try`内で`reject`と記述し、`catch`を後につけるとその中の処理が実行される。なお`e`はエラーのことで慣習的につけている。

[![Image from Gyazo](https://i.gyazo.com/5ba40a23aa83de6cd3a673e98d52aa78.png)](https://gyazo.com/5ba40a23aa83de6cd3a673e98d52aa78)