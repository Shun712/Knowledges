# なぜstateを使うのか

- Reactコンポーネント内の値を書き換えたいとき

  - コンポーネント内の要素をDOMで直接書き換えてはいけない（x）

  - 新しい値を使って再描画（再レンダリング）させる(o)

- Reactコンポーネントが再描画するタイミングはいつか?

  - stateが変更されたとき

  - propsが変更されたとき

# userState(Reactのメソッド)の使い方

[![Image from Gyazo](https://i.gyazo.com/35e576afce22d752ce163cc12a314ea5.png)](https://gyazo.com/35e576afce22d752ce163cc12a314ea5)

# propsとstateの違い

両者とも再描画のきっかけになるが...

- propsは引数のようにコンポーネントに渡される値(親から子へ渡される場合)

- stateはコンポーネントの内部で宣言・制御される値(子内部で値を変更できる)

# stateをpropsに渡す

[![Image from Gyazo](https://i.gyazo.com/0dcc017964e7689f075cdb68f7d10c84.png)](https://gyazo.com/0dcc017964e7689f075cdb68f7d10c84)

[![Image from Gyazo](https://i.gyazo.com/55142212caebf4ed61d0fdc315ac35da.png)](https://gyazo.com/55142212caebf4ed61d0fdc315ac35da)

# 注意点

[![Image from Gyazo](https://i.gyazo.com/f50973c0c1610eeb0187b06aaebb939b.png)](https://gyazo.com/f50973c0c1610eeb0187b06aaebb939b)

無限ループを起こして、エラーになる。

# Stateの具体例

1. 文字入力

[![Image from Gyazo](https://i.gyazo.com/524ff2026c22ef215f7540561f2c839f.png)](https://gyazo.com/524ff2026c22ef215f7540561f2c839f)

[![Image from Gyazo](https://i.gyazo.com/d31c1dd695a8e53c42b46271e6a579d2.png)](https://gyazo.com/d31c1dd695a8e53c42b46271e6a579d2)

2. カウンター(prevState)

[![Image from Gyazo](https://i.gyazo.com/0dcb4f389e90a646e52acc9f2b288c2d.png)](https://gyazo.com/0dcb4f389e90a646e52acc9f2b288c2d)

3. ON/OFFを切り替え

[![Image from Gyazo](https://i.gyazo.com/eefa3e5c364f32b4de586600ff58aa85.png)](https://gyazo.com/eefa3e5c364f32b4de586600ff58aa85)

# 参考

[#06 新・日本一わかりやすいReact入門【基礎編】コンポーネントの状態管理](https://www.youtube.com/watch?v=dTghhYtvPek&t=248s)