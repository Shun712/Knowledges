# useReducerの使い方

1. `rstate`に`state`の値が入る

2. `useReducer`の第一引数では、`dispatch`の関数が走る。また、`state`の更新をどのようにするか定義する。

3. `useState`との違いはコールバック関数に処理を記述するが、`useReducer`は定義の時点で処理を記述する。

4. `useReducer`の第2引数には初期値が入る。

[![Image from Gyazo](https://i.gyazo.com/2fdc321407d0080d3c7b98efd7969d25.png)](https://gyazo.com/2fdc321407d0080d3c7b98efd7969d25)

# useStateとuseReducerの違い

複雑度合いで決める。
`useState`->`useReducer`->`Redux`  
`useState`: 状態の更新の仕方は利用側に託す。
`useReducer`: stateと一緒に更新用の処理を保持。

[![Image from Gyazo](https://i.gyazo.com/c798f79debc30f3cc0e33feff9c8b2a4.png)](https://gyazo.com/c798f79debc30f3cc0e33feff9c8b2a4)

- 純粋性（純粋関数）
- 特定の引数に特定の戻り値
- 不変性

# useContext

- 孫までpropsを引き渡す際に、propsのバケツリレーを回避する。

[![Image from Gyazo](https://i.gyazo.com/8a11726f2f57214a469f6f24b1e84986.png)](https://gyazo.com/8a11726f2f57214a469f6f24b1e84986)

- stateをコンポーネント間で共有したい場合は、`<Context.Provider />`で囲む。

1. 元となるコンポーネントで`createContext`を定義する。

2. `export const MyContext = createContext();`と変数を設定し、使用したいコンポーネントで取得する。（変数は自由に変えて良い。）

3. `useState`を用いて分割代入をそれぞれのコンポーネントで状態を管理している。

[![Image from Gyazo](https://i.gyazo.com/9bb7d5ecbc7e04131fe0a06f70409dcf.png)](https://gyazo.com/9bb7d5ecbc7e04131fe0a06f70409dcf)

[![Image from Gyazo](https://i.gyazo.com/e912895c65affab80385b883ca121c54.png)](https://gyazo.com/e912895c65affab80385b883ca121c54)

- useContextを使いたい場合、`<ThemeContext.Provider>`で挟みたいものは、`children`を持ってくる。

[![Image from Gyazo](https://i.gyazo.com/3474edd93502095ddf702ed750307344.png)](https://gyazo.com/3474edd93502095ddf702ed750307344)
