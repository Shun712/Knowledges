# 3種類のライフサイクル

[![Image from Gyazo](https://i.gyazo.com/962b40cad5582697f67ef5fcc28e037d.png)](https://gyazo.com/962b40cad5582697f67ef5fcc28e037d)

- Mounting

コンポーネントが配置される（生まれる）期間  
最初サイト上に画面が描画されるとき

- Updating
コンポーネントが変更される（成長する）期間
何かしらの変更が加えられてるとき

- Unmounting
コンポーネントが破棄される（死ぬ）期間
ページ遷移するとき

# 副作用(effect)フックの概念

[![Image from Gyazo](https://i.gyazo.com/ba4646f8ffe15406757538ef78c342a5.png)](https://gyazo.com/ba4646f8ffe15406757538ef78c342a5)

`useEffect`でカウントされるたびに、ログが吐き出される。

# 参考

[#08 新・日本一わかりやすいReact入門【基礎編】ライフサイクルと副作用を理解しよう](https://www.youtube.com/watch?v=f8iXdpbvvH8)