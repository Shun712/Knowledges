# pathを通すとは?

コマンド検索パス(コマンドサーチパス)を追加すること

# コマンド検索パスとは?

シェルが**コマンド実行ファイルを探しに行くパス**のこと

```
# どちらのコマンドでも同じ結果が出力される。
/bin/ls
ls
```
`ls`を入力された時に探しに行った`/bin`ディレクトリに同じ名前の実行ファイルが存在したため、それが実行された。

# コマンド検索パスの確認方法

コマンド検索パスは環境変数`$PATH`に設定されており、`echo $ PATH`で確認できる。

```
echo $PATH
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/sbin #実行結果
```
パスは`:`で区切られており、今回の例では下記のパスがコマンド検索パスとして設定されている。

```
/usr/local/bin
/usr/bin
/bin
/usr/sbin
/sbin
/usr/local/sbin
```

# コマンド実行ファイルの格納場所の確認方法

`which`を利用すれば指定したコマンドの実行ファイルがどこに格納されているか確認できる。

```
which ls
/bin/ls #実行結果
```

# 同じ名前のコマンド実行ファイルが複数のコマンド検索パスに存在する場合

コマンド検索パスには優先度があり、`echo $ PATH`で出力された左が優先される。

# PATHの通し方

`~/.bashrc`や`~/.bash_profile`に以下のコマンドを記述する。(記述はどちらかで良い。)

```
(# .bashrc)
export PATH=$PATH:追加したいコマンド検索パス

(# .bash_profile)
export PATH=$PATH:追加したいコマンド検索パス
```
記述後は編集したファイルに対して`source`コマンドを実行しないとPATHが通らない.

```
source ~/.bashrc
source ~/.bash_profile
```

# exportコマンドとは?

1. 環境変数を**表示**できる
2. 環境変数を**設定**できる

### 1. 環境変数を表示する

```
export -p

#出力結果(一部のみ記載)
declare -x PATH="/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
declare -x LANG="ja_JP.UTF-8"
declare -x SHELL="/bin/bash"
```

### 2. 環境変数を設定する

例えば、`$URB`という環境変数を設定する。

```
export ULB=/usr/local/bin
```

環境変数`$URB`が設定されたので`echo $URB`で確認できる。

```
echo $ULB
/usr/local/bin #出力結果
```
設定した環境変数を利用してみる。

```
#どちらのコマンドでも同じ結果が出力される。
ls /usr/local/bin
ls $ULB
```

# exportを理解した上で再度PATHを通す記述を確認してみる。

環境変数`$PATH`を上書き(再記述)して設定する。

```
export PATH=$PATH:追加したいコマンド検索パス
```
`$PATH`を記述しなくても以下のように記述すれば同じ

```
#現在$PATHに設定されているコマンド検索パスが以下の場合
#/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/sbin

#どちらの記述でも$PATHに設定されるコマンド検索パスは同じ。
export PATH=$PATH:追加したいコマンド検索パス
export PATH=/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/sbin:追加したいコマンド検索パス
```

# 追加するコマンド検索パスの優先度を高くしたい

```
export PATH=追加したいコマンド検索パス:$PATH
```

# 参考

[PATHを通すとは？ (Mac OS X) - qiita](https://qiita.com/soarflat/items/09be6ab9cd91d366bf71)

[PATHを通すために環境変数の設定を理解する (Mac OS X) - qiita](https://qiita.com/soarflat/items/d5015bec37f8a8254380)
