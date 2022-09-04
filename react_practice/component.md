# コンポーネントとは

見た目と機能を持つUI部品である。例えば、再生ボタンを押すと、同時に動画が再生されるなど。

今では、`Functional Component(関数コンポーネント)`が主流である。  
メリットとしては、記述量が少ない。

[![Image from Gyazo](https://i.gyazo.com/9a3c770cbb56f5c026da5129ed8e2694.png)](https://gyazo.com/9a3c770cbb56f5c026da5129ed8e2694)

# なぜコンポーネントを使うのか?

- コードを再利用するため

- コードの可読性を上げるため

  - 1コンポーネント = 1ファイル

  - 別ファイルに分けてコードを読みやすくする

- 修正・変更に強い

# 使い方

[![Image from Gyazo](https://i.gyazo.com/c425bf91f4e1f627c8e5128d12460859.png)](https://gyazo.com/c425bf91f4e1f627c8e5128d12460859)

- ファイル名は大文字にする

- 子コンポーネントで`export`

- 親コンポーネントで`import`

# propsでデータを受け渡す

[![Image from Gyazo](https://i.gyazo.com/7d2c8b44a2983c34c0296075fa431f58.png)](https://gyazo.com/7d2c8b44a2983c34c0296075fa431f58)

- 子コンポーネントの引数に`props`を指定する

- **親から子に**データを渡す

※ver17から`import Article from ......`は記述不要になった。

# 参考

[#04 新・日本一わかりやすいReact入門【基礎編】コンポーネントとprops](https://www.youtube.com/watch?v=Q-df0QgZuhE&t=12s)