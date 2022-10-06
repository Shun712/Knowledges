# TypeScriptの特徴

- JSに変換してから実行

- 型の定義が可能

- JSにない記述が使用可能

[![Image from Gyazo](https://i.gyazo.com/4f9b71bb77ccf0d5844bba248b703de1.png)](https://gyazo.com/4f9b71bb77ccf0d5844bba248b703de1)

[![Image from Gyazo](https://i.gyazo.com/bdcbaa09b6b9cf08fb584c5e8b8ac9f1.png)](https://gyazo.com/bdcbaa09b6b9cf08fb584c5e8b8ac9f1)


- リテラル型は特定の文字列や数値、真偽値などを定義することができる。

[![Image from Gyazo](https://i.gyazo.com/4b2076e8f5e24500f131e2fcf546993f.png)](https://gyazo.com/4b2076e8f5e24500f131e2fcf546993f)

# ユニオン型

- 複数の型を組み合わせて、「または」の意味を表すことができる。

[![Image from Gyazo](https://i.gyazo.com/8e32a9fc5a5944c24ca419073552261d.png)](https://gyazo.com/8e32a9fc5a5944c24ca419073552261d)

# オブジェクト型の定義

```typescript
const arr1: number[] = [1, 2, 3];
const arr2: string[] = ['Hello', 'bye'];
const arr3: Array<number> = [1, 2, 3];
const arr4: (string | number)[] = [1, 'bye'];
const arr5: Array<number | string> = [1, 'bye'];

// オブジェクトの型を決める
const obj1: { name: string, age: number } = {name: 'Taro', age: 12};
  obj1.name = 18;

// ?はそのプロパティがなくてもいい
type Person = { name: string, age?: number }
const obj2: Person = {name: 'Taro'}

const users: Person[] = [
  {name: 'Taro'},
  {name: 'Hanako', age: 30},
]
```

# typescriptの型推論

- 明らかに型がわかるような場合の型定義は型推論に任せるようにする

[![Image from Gyazo](https://i.gyazo.com/90b00fb5f0c2c3d7e60c3b885f0b5674.png)](https://gyazo.com/90b00fb5f0c2c3d7e60c3b885f0b5674)

# 型のエイリアス

- 型を定義するときはパスカルケース（先頭大文字）で書く。

[![Image from Gyazo](https://i.gyazo.com/e0cda22d7ccbcfd30155b57449b36d6d.png)](https://gyazo.com/e0cda22d7ccbcfd30155b57449b36d6d)

# 関数の型定義

- 引数は型を定義しなければいけない。

- 以下のようにデフォルト値も設定できる。

```typescript
function sum1(x: number, y: number = 1) {
  return x + y;
}
```
- 引数の後に型を定義する

[![Image from Gyazo](https://i.gyazo.com/b41a60ddb57157bc1b0d7ea415a92ea7.png)](https://gyazo.com/b41a60ddb57157bc1b0d7ea415a92ea7)

# ジェネリクスの型定義

- 型を引数のようにして取り扱う。型は関数実行時に決定する。

[![Image from Gyazo](https://i.gyazo.com/5eb3a3a976ceac37a0e0dbd89b3f68fb.png)](https://gyazo.com/5eb3a3a976ceac37a0e0dbd89b3f68fb)

- しかし、関数実行時の方のジェネリクスの型定義は省略された形が多い。

[![Image from Gyazo](https://i.gyazo.com/457a74a8f1213abe22dd8a7979e40705.png)](https://gyazo.com/457a74a8f1213abe22dd8a7979e40705)

# 関数コンポーネントで型を導入

- namespace(名前空間)とは、コードを整理するための手法

- typescriptでReactを用いる際は**関数コンポーネント**を定義する。

[![Image from Gyazo](https://i.gyazo.com/14096f6f7d20cbae6ffb3c857f54271d.png)](https://gyazo.com/14096f6f7d20cbae6ffb3c857f54271d)

# propsの型定義

- ジェネリクスがない場合、`P`は空になり、ある場合は`P`にそのジェネリクスが代入される。

[![Image from Gyazo](https://i.gyazo.com/3c13220d385db835e81411e98285e271.png)](https://gyazo.com/3c13220d385db835e81411e98285e271)

- コンポーネントタグに挟まれたものの型を定義すると`ReactNode`

- 型は関数型も定義できる。

[![Image from Gyazo](https://i.gyazo.com/7ece90e7c42a4dbfd0fffa4a02839e1b.png)](https://gyazo.com/7ece90e7c42a4dbfd0fffa4a02839e1b)

# classの型定義方法

- `public`はどこからでもアクセス可

- `private`はクラス外からアクセス不可

- `protected`はクラスと子コンポーネント外はアクセス不可

[![Image from Gyazo](https://i.gyazo.com/e17ea9bf5bc8ff3181d79f5e54cf23d2.png)](https://gyazo.com/e17ea9bf5bc8ff3181d79f5e54cf23d2)

