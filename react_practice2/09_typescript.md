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