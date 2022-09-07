# ルーティングの基礎

- `BrowserRouter`は、Reactプロジェクトの中で一度しか使えない。

- `React Router`は`BrowserRouter`の中でしか使えない。

下記で以下の3つのURLにアクセスできる。
```
localhost:3000

localhost:3000/register/

localhost:3000/login/
```

```javascript
/* App.js */

// react-router-dom」から以下の3つをimportする
import { BrowserRouter, Routes, Route } from "react-router-dom";

import Home from "./Home";
import Register from "./Register";
import Login from "./Login";

const App = () => {
  return (
    <BrowserRouter>
      <Routes>
        <Route path={`/`} element={<Home />} />
        <Route path={`/register/`} element={<Register />} />
        <Route path={`/login/`} element={<Login />} />
      </Routes>
    </BrowserRouter>
  );
};

export default App;
```

# ルーティングしたときにpropsを渡す方法

`props`とは親・子コンポーネント間でのデータの「受け渡し口」のようなものである。  
**親コンポーネントから渡したいデータ**を`props`という箱に入れ、子コンポーネントも`props`という箱を受け取れるようにし、**子コンポーネントの中で**propsの箱の中のデータを参照する。

```javascript
export const ChildComponent = (props) => {
  // (1) props.idの方法で取得する方法
  const hoge = () => { props.id }
}
```

```javascript
export const ChildComponent = ({ id }) => {
  // (2) idと直接key名を指定してデータを参照する方法
  const hoge = () => { id }
}
```

# 参考

[【最新バージョン対応】React Routerの使い方を解説](https://ralacode.com/blog/post/how-to-use-react-router/)