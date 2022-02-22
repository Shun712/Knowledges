# 15 モデルスペックを実装

## やったこと
## RSpec
RubyにおけるBDD（振舞駆動開発）のためのテスティングフレームワークである。

## テストを書くためのメリット
開発した機能を確認するために、テストを書くことが大切である。自分がどのように動くコードを書いているのかを記録に残し、常に動くことを確認しながら開発ができるので、確実性を高めることができ最終的に開発時間を節約してくれる。

## モデルスペックとは?
モデルが正しく機能しているかテストし、バリテーションに使われることが多い。
また、モデルのメソッドが期待通りに動作するかテストする。

## Factory Botとは?
テスト用データの作成をサポートするgemである。`ActiveRecord`モデルに実装したコールバックなどの資産を直接的に活用してデータの状態やデータ間の関係性などを制御しやすくなる。

> [Factory Botとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/15_model_spec/index/factory_bot.md)

## simplecovとは?
Rspecで書いたテストのカバレッジを算出するツールである。カバレッジとは、コード全体に対して、どの程度の範囲をテストが網羅されているかを計測したものである。

## 学んだこと
```ruby
1) User インスタンスメソッド like? いいねをした投稿が含まれること
     Failure/Error: expect { user_a.like?(post_by_user_b) }.to be true
       You must pass an argument rather than a block to `expect` to use the provided matcher (equal true), or the matcher must implement `supports_block_expectations?`.
```
expectに渡すのは、ブロック（中括弧）ではなく丸括弧である。
- `change`マッチャや`raise_error`マッチャは、expectにブロック（中括弧）を渡す。
- それ以外は、丸括弧で渡す。

```ruby
 1) User インスタンスメソッド like? いいねをした投稿が含まれること
     Failure/Error:
       before do
         user_a.like(post_by_user_b)
         user_a.like(post_by_user_c)
       end

       `before` is not available from within an example (e.g. an `it` block) or from constructs that run in the scope of an example (e.g. `before`, `let`, etc). It is only available on an example group (e.g. a `describe` or `context` block).
```
`it`ブロック内では、`before`ブロックは使えない。使用する場合は、`describe`や`context`内のブロックで定義する。