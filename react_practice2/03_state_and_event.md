# イベントハンドラー

- `onClick`に渡すのは、`clickHandler`の関数であって、`clickHandler()`とするとJSXを実行するときに関数が実行されてしまう。

[![Image from Gyazo](https://i.gyazo.com/00e40414d9cb7255705e087ba12ffc87.png)](https://gyazo.com/00e40414d9cb7255705e087ba12ffc87)

- 以下も同じであるが、アロー関数を定義するときと似た書き方になる。

[![Image from Gyazo](https://i.gyazo.com/314955f8d67259bd3d4bdfa7880704ee.png)](https://gyazo.com/314955f8d67259bd3d4bdfa7880704ee)

- JavaScript関数と名前が違うので注意！

- `input`タグと一緒に用いるのは主に、
  - `onChange`は入力されるたびに発火する
  - `onBlur`は入力欄から離れると発火する
  - `onFocus`は入力欄をクリックすると発火する

- `onMouseEnter`は所定の位置にマウスがホバーすると発火

- `onMouseLeave`は所定の位置からマウスが離れると発火

[![Image from Gyazo](https://i.gyazo.com/453670d8e63e185ce6116532425cdc4e.png)](https://gyazo.com/453670d8e63e185ce6116532425cdc4e)

# useState

- `useState`はinportが必要

- `useState`の配列`['参照用の値', '更新用関数']`

[![Image from Gyazo](https://i.gyazo.com/b00b11812ab42161c20d7c31118d5527.png)](https://gyazo.com/b00b11812ab42161c20d7c31118d5527)

# ステートとは?

- React内部に保持されたコンポーネントに紐づく値を`state`と呼ぶ。

- あくまで`state`はコンポーネント単位で保持される

- コンポーネント内に定義した変数はレンダリングの度に**初期化され保持されない**。

[![Image from Gyazo](https://i.gyazo.com/a95f528c56ced6f01a26d7a3072d929c.png)](https://gyazo.com/a95f528c56ced6f01a26d7a3072d929c)

[![Image from Gyazo](https://i.gyazo.com/950f272b9454c3773d96dc62e5b4f6b7.png)](https://gyazo.com/950f272b9454c3773d96dc62e5b4f6b7)

- `setVal`が呼び出される度に、`Example`の関数が呼び出される。

[![Image from Gyazo](https://i.gyazo.com/75a70532280f28b7bc512f4067f1ea92.png)](https://gyazo.com/75a70532280f28b7bc512f4067f1ea92)

# state使用時の注意点

- stateは、コンポーネントの`トップレベル`内でしか使えない。if、while文内でも不可。

[![Image from Gyazo](https://i.gyazo.com/de93d25695dc0d49fda165e2b415c8cf.png)](https://gyazo.com/de93d25695dc0d49fda165e2b415c8cf)

- `count`の値はすぐ値が更新されるのではなく、まずreact内部へ値の更新を予約する。

1. 初期値が描画される

2. カウントをクリックする

3. `setCount`更新関数が呼び出され、カウントアップした値をReact内部に保持される。

4. 再レンダリングした際に、`count`した値を取ってきて描画する。

[![Image from Gyazo](https://i.gyazo.com/ea7f7888ad42162908bef6a23f576e28.png)](https://gyazo.com/ea7f7888ad42162908bef6a23f576e28)

[![Image from Gyazo](https://i.gyazo.com/a876bc511b4f3652f533ff398441e807.png)](https://gyazo.com/a876bc511b4f3652f533ff398441e807)

# オブジェクトのステートは新しいオブジェクトを設定する

- `setPerson`(更新用関数)に渡すべきオブジェクトは`person`(現在の値)と**異なるオブジェクト**である必要がある。ゆえにプロパティを設定しただけだと、**オブジェクトは変わらない**。

**ダメな例**
[![Image from Gyazo](https://i.gyazo.com/c6a09ef7539e79a0a3dac482286f42be.png)](https://gyazo.com/c6a09ef7539e79a0a3dac482286f42be)

- オブジェクトの値を変更するには、新しいオブジェクトを生成して、そのプロパティに新しい値を設定する。
`name: e.target.value`

- スプレッド演算子を用いて、**新しいオブジェクトとして**生成される。さらに、スプレッド演算子で展開されたプロパティを上書きするには、更新したいプロパティを追加する。

[![Image from Gyazo](https://i.gyazo.com/016dc256fc5796b975a1f9e763e8309e.png)](https://gyazo.com/016dc256fc5796b975a1f9e763e8309e)

- 正しい記述は、コールバック関数で書いてあげる。戻り値(`{...order, item: e.target.value}`)がオブジェクトのアロー関数となる。

[![Image from Gyazo](https://i.gyazo.com/6c81da97c817cc1d49eee38f4451599f.png)](https://gyazo.com/6c81da97c817cc1d49eee38f4451599f)

# 配列のステートを扱う際の注意

- `newNums = nums`と`newNums = [...nums]`は真偽値が異なる。前者は値を参照しているだけだが、後者は配列の値を一つ一つ展開している。

- `pop`は配列の最後の要素を削除する。`unshift`は配列の先頭に引数の値を挿入する。

[![Image from Gyazo](https://i.gyazo.com/d3cf61130df6ae6f228c15f02e339810.png)](https://gyazo.com/d3cf61130df6ae6f228c15f02e339810)

# ステートとコンポーネントの関係

- ツリー構造が同じ枝だと`state`の値は保持されるが、枝分かれした場合は値がリセットされる。

- 同じ枝だが、分けて値を管理したい場合は、`key`プロパティを用いる。

[![Image from Gyazo](https://i.gyazo.com/e1dc2bc70999a6646f41225f69e5971b.png)](https://gyazo.com/e1dc2bc70999a6646f41225f69e5971b)

[![Image from Gyazo](https://i.gyazo.com/4773d067c81c8f0a32b4f3503927ecfe.png)](https://gyazo.com/4773d067c81c8f0a32b4f3503927ecfe)

[![Image from Gyazo](https://i.gyazo.com/c90ba2d65039e3a0af100f6ce3de008c.png)](https://gyazo.com/c90ba2d65039e3a0af100f6ce3de008c)

[![Image from Gyazo](https://i.gyazo.com/1e42f838e9e30538f8ae5b7082792cf0.png)](https://gyazo.com/1e42f838e9e30538f8ae5b7082792cf0)

# ステートを複数のコンポーネントで管理

- `state`を`props`で渡すのはコンポーネントが消滅するときや、特定のstateを複数の子コンポーネントで共有したいときである。

- `prevState`は現在の値に何らかの処理をする。

- コールバック関数の引数には、現在のstateが入る。

[![Image from Gyazo](https://i.gyazo.com/5d0b2bc9b12e243c93521167d43caf96.png)](https://gyazo.com/5d0b2bc9b12e243c93521167d43caf96)