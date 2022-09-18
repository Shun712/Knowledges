# ポータル

- `createPortal`で親要素に対して子要素を付け足せる。

- `createPortal`は主に、モーダル、ポップアップ、トーストで併用され、親要素を無視して表示できる。

- `<div className="container start">ココ！！</div>`にマウントしている。

- `createPortal`を付けると指定した`<div className="container start">ココ！！</div>`に表示できる。


[![Image from Gyazo](https://i.gyazo.com/890c0de2b74dea8af2b374dfd488bb21.png)](https://gyazo.com/890c0de2b74dea8af2b374dfd488bb21)

[![Image from Gyazo](https://i.gyazo.com/2be0fb472a2f09f661956e1a5b607858.png)](https://gyazo.com/2be0fb472a2f09f661956e1a5b607858)

# useRefでDOMを直接操作する

- useRefで注目したいDOM要素を指定する

[![Image from Gyazo](https://i.gyazo.com/67a49cc3ca4793318bba30b72017cac0.png)](https://gyazo.com/67a49cc3ca4793318bba30b72017cac0)

- refの値を変更しても再レンダリングがトリガーされない。(同じく値を保持できる`state`は変更されると再レンダリングされる。)

- refオブジェクトをJSXのref属性に渡すとそのDOMにアクセスできる。

[![Image from Gyazo](https://i.gyazo.com/bf3bc5e48c5eb73295f2eeb737bb00bd.png)](https://gyazo.com/bf3bc5e48c5eb73295f2eeb737bb00bd)

# 他のコンポーネントのDOMにアクセスする方法

- `ref`はpropsとして渡せないので、別の方法が必要である。

- `forwardRef`という関数を用いて渡せる。

- 親から子へのデータの受け渡しはOKだが、子から親へは基本NGである。双方向に行き来してしまうからである。

[![Image from Gyazo](https://i.gyazo.com/4c99ebd692f72f7db999d6f61ab8cb19.png)](https://gyazo.com/4c99ebd692f72f7db999d6f61ab8cb19)

# useImprativeHandleを使う

- 動画再生のときなどで使う

[![Image from Gyazo](https://i.gyazo.com/4d18424575bc66ce526b6647cec6e68c.png)](https://gyazo.com/4d18424575bc66ce526b6647cec6e68c)

# まとめ

[![Image from Gyazo](https://i.gyazo.com/1b9d386792bd0e80e257f4a913d1e735.png)](https://gyazo.com/1b9d386792bd0e80e257f4a913d1e735)