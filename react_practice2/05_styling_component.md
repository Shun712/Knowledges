# インラインスタイルの使い方

- 文字列のプロパティは`" "`を忘れずに。

- `<button style={style}>`のようにタグ内に`style`を埋め込む。

- js内だと`px`要らない。

- 再利用性が悪くなる。パフォーマンスも悪くなる。

[![Image from Gyazo](https://i.gyazo.com/cf4f3f0512c8a28fea715d69e259ae4a.png)](https://gyazo.com/cf4f3f0512c8a28fea715d69e259ae4a)

# 外部CSSのimportを使う

- `import "./Example.css"`でCSSファイルを読み込む。ファイル名はコンポーネントと同じにする。

- `<button className>`でCSSファイル内のクラス名に当てはまるスタイルを呼び出す。

- componentごとにCSSは読み込めない。CSSは後から読み込まれたものが反映される。また、同じクラス名だと値が上書きされる。

[![Image from Gyazo](https://i.gyazo.com/1ba97a34b6e742b1cd9101022d59bc21.png)](https://gyazo.com/1ba97a34b6e742b1cd9101022d59bc21)

# CSSモジュールの使い方

- 将来廃止される。

- componentごとにスタイルを反映できる。

# CSS-in-JS　の使い方

- 生成する要素を指定し、スタイルをテンプレートリテラルで記述する。

- valueを関数にすることで、引数にpropsを渡すことができる。動的にスタイルを変更できる。

- `{isSelected}`の部分を変更することで受け取るクラス名を変更できる。

[![Image from Gyazo](https://i.gyazo.com/1707dd84b67c505af93a0c4b592b4e33.png)](https://gyazo.com/1707dd84b67c505af93a0c4b592b4e33)

- スタイルを継承し、`styled()`でラップする。

- スタイルは上書きできる。

- `hover`や`span`でスタイル変更できる。

[![Image from Gyazo](https://i.gyazo.com/d951a4655e25933b7cd7c84b9625f87c.png)](https://gyazo.com/d951a4655e25933b7cd7c84b9625f87c)

- propsの渡し方は`background-color: ${(props.dark) => dark ? "black" : "green"};`でも可。

[![Image from Gyazo](https://i.gyazo.com/103dc878c12e5f98d88e8e6ea66d0a10.png)](https://gyazo.com/103dc878c12e5f98d88e8e6ea66d0a10)

# 様々なスタイル

- ChakraUI

- MaterialUI

- Tailwind
