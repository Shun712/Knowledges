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
`useReducer`: stateと一緒に更新用の処理を保持
