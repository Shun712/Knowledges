# Goの基礎知識まとめ

- ポインタの理解を深める

# ポインタとは

- コンピューターには`メモリ`と呼ばれる作業場所が存在する。

- 変数はそのメモリに記録されており、その場所を`アドレス`と呼ぶ

[![Image from Gyazo](https://i.gyazo.com/a606ab07aa1d20b983cfe869fe5e3f6d.png)](https://gyazo.com/a606ab07aa1d20b983cfe869fe5e3f6d)

- `fmt.Println(&〇〇)`で変数〇〇のアドレスを取得できる

- `Go`ではアドレスを`ポインタ`と呼んで扱っている

- ポインタが代入された変数を`ポインタ型変数`と呼ぶ

# ポインタ型変数の定義

- ポインタ型変数を定義するには、変数のデータ型「`*(アスタリスク)`」をつけて宣言する

[![Image from Gyazo](https://i.gyazo.com/c4ad84401261a7f9866fcd3f43b853a0.png)](https://gyazo.com/c4ad84401261a7f9866fcd3f43b853a0)

# ポインタからアクセスする

- ポインタ型変数に対して「`*(アスタリスク)変数名`」として、そのポインタから示す変数の値を取り出せる

[![Image from Gyazo](https://i.gyazo.com/11cbc2d3105fbcce95428defcdc606c5.png)](https://gyazo.com/11cbc2d3105fbcce95428defcdc606c5)

[![Image from Gyazo](https://i.gyazo.com/5b8c3fd99993d44126472a30338f18a9.png)](https://gyazo.com/5b8c3fd99993d44126472a30338f18a9)

```go
package main

import "fmt"

func main() {
	totalScore := 0
	// 引数にtotalScoreのポインタを渡してください
	ask(1, "dog", &totalScore)
	ask(2, "cat", &totalScore)
	ask(3, "fish", &totalScore)

	fmt.Println("スコア", totalScore)
}

// 渡されるtotalScoreのポインタを受け取るように変更してください
func ask(number int, question string, scorePtr *int) {
	var input string
	fmt.Printf("[質問%d] 次の単語を入力してください: %s\n", number, question)
	fmt.Scan(&input)

	if question == input {
		fmt.Println("正解!")
		// ポインタを使って加算してください
		*scorePtr += 10
		
	} else {
		fmt.Println("不正解!")
	}
}
```