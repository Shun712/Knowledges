# rubocopとは？

Rubyの静的コード解析を実行するgemであり、インデントやメソッド名、改行などのチェックをしてくれるものである。

# 関連ファイル

**.rubocop.yml**

rubocopの設定ファイルで、対象となるファイルの種類だったり、チェックする構文のデフォルトを変えたり、自分たちのコーディングスタイルに沿ったルールをこのファイルで適用できる。

**.rubocop_todo.yml**

あまりに警告が多い時に`$ rubocop --auto-gen-config`を実行することによって自動生成され、警告内容を全てこのファイルに一旦退避することができる。

# 基本コマンド

```
$ rubocop
# 解析して結果をターミナルに吐き出す。

$ rubocop --help
# ヘルプを参照できます。

$ rubocop --lint( または rubocop --rails )
# チェック規則は以下の4つに分類されますが --lint がLintのみチェック、 --rails がRailsのみチェック
# -------------------------------------------------------------------------
# 1 Style   (スタイルについて)
# 2 Lint    (誤りである可能性が高い部分やbad practiceを指摘する)
# 3 Metrics (クラスの行数や1行の文字数などに関して)
# 4 Rails   (Rails特有のcop)

$ rubocop --auto-gen-config 
# .rubocop_todo.ymlに警告を一旦退避する。
# .rubocop.ymlに "inherit_from: .rubocop_todo.yml" と書くのを忘れないでください。

$ rubocop --auto-correct 
# 直せる箇所を自動で修正してくれます。(最初は使わないで警告されたコードを眺めてみることをお勧めします。)
```

# 修正の流れ

> ⓪ `$ rubocop --auto-correct`を実行して、自動で修正できるものはしてもらう。残りの警告がたくさんある場合は①へ。警告がそんなに多くない場合(10 ~ 20個とか)は③と④を繰り返す。
> Railsのコード規則を学ぶのにとても良い教材だと思うので初めは⓪を飛ばすことをお勧めします。)

> ① 警告がたくさんあると見ずらいので`$ rubocop --auto-gen-config`を実行し、`.rubocop_todo.yml`を作成し、そこに全ての警告をいったん移す。(こうすることで`$ rubocop`を実行しても今の段階では全ての警告は無視されます。)

> ② `.rubocop_todo.yml`内の警告の中から一番上の警告をコメントアウトする。(コメントアウトした警告だけが再びRuboCopに感知されるようになる)

> ③ `$ rubocop`を実行して警告を修正する。

> ④ 警告のデフォルトを変更したり、特定のファイルを今後RuboCopに警告されないたくないという場合は, `.rubocop.yml`に設定を書く。

> ⑤ 修正し終わったら`.rubocop_todo.yml`に戻り、コメントアウトした警告を削除する。

> ⑥ `.rubocop_todo.yml`内全ての警告を修正し終わるまで② ~ ⑤を繰り返す。

> ⑦ テストがある場合はテストを走らせる。

> 引用[RuboCop is 何？](https://qiita.com/tomohiii/items/1a17018b5a48b8284a8b)

# 忘れがちになるための対策
開発を進めていくと、rubocop機能は忘れがちになるので注意が必要である

> [【Ruby on Rails】rubocop と pre-commit を利用して git commit 時にコーディングチェックを行う](https://techblog.kyamanak.com/entry/2018/06/19/221910)

# 参考
[RuboCop is 何？](https://qiita.com/tomohiii/items/1a17018b5a48b8284a8b)
[[rails] rubocopとは？](https://qiita.com/freestylehh46/items/f8dae4b962df681ed2ad)