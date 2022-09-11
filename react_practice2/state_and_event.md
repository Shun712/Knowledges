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