# Reactアプリケーションにおけるスタイルのあて方

Reactのコンポーネントに対してスタイルを当てる方法は以下の3つである。

1. JSXに対してclass(className)を使ってCSSを当てる方法

2. CSSをmodule化する方法

3. CSS in JS

Material UIというUIフレームワークを使う場合は、`CSS in JS`が相性が良い。

今回は `CSS in JS` のライブラリの中でも`styled-components`を使う。

# styled-componentsの書き方

```javascript
const Link = () => (
  <a href="/">
  　リンク
  </a>
)
```
このリンクに`styled-components`であてるには以下のようになる。

```javascript
import styled from 'styled-components';

const Button = styled.a`
  display: inline-block;
  border-radius: 3px;
  padding: 0.5rem 0;
  margin: 0.5rem 1rem;
  width: 11rem;
  background: transparent;
  color: white;
  border: 2px solid white;
`;
```

# メリット

- css, class, id の管理が(比較的)楽になる
- ローカルスコープなスタイルができる

# デメリット

- パフォーマンスの低下につながる書き方ができてしまう
- エディタによってはCSSが補完されない

# 参考

[styled-components - 公式](https://styled-components.com/)