# ルーティングした際のpropsの渡し方

ルーティングは、`react-router-dom v6`で設定する。
コンポーネントに`props`を渡し、パラメータを取得する`useParams`をインポートする。

```javascript
# App.jsx

import React from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import { User } from './containers/User';


function App() {
  return (
    <Router>
    {/* <Router>で<Routes>を囲む */}
    <Routes>
      {/* path="Url" element={コンポーネント} */}
      {/* urlに:keyを記述 */}
      <Route path="user/:id" element={<User />} />
    </Routes>
  </Router>
  );
}
export default App;
```

```javascript
# User.jsx

import React from 'react'
import { useParams } from 'react-router-dom'

export const User = () => {
  // useParamsでパラメーターを受け取ることができる
  const { id } = useParams()
  return (
    <>
      <div>ユーザー情報画面</div>
      <p>ユーザーIDは{id}です。</p>
    </>
  )
}
```

# 参考

[【React】ルーティングした際にpropsを渡す方法 - qiita](https://qiita.com/P-man_Brown/items/4957eee5eae3155d0528)