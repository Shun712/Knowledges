# 07 投稿の検索機能を実装する

# やったこと
- 全ての投稿を検索対象とすること（フィードに対する検索ではない）
- 検索条件としては以下の三つとする
  - 本文に検索ワードが含まれている投稿
    - こちらに関しては半角スペースでつなげることでor検索ができるようにする。e.g.「rails ruby」
  - コメントに検索ワードが含まれている投稿
  - 投稿者の名前に検索ワードが含まれている投稿
- ransackなどの検索用のGemは使わず、フォームオブジェクト、ActiveModelを使って実装すること
- 検索時のパスは/posts/searchとすること

# Form Objectとは?
Ruby on Railsのデザインパターン「設計手法」の1つである。
もともと、modelにバリテーションなど様々な処理が書かれているものを、form層に切り出すことで多くのmodelで同一の処理を使えるなど、拡張性の高いコードを実現させることができる。

Form Objectを使う場面というのは、
複数のモデルに跨がる場合、もしくはDBに保存する必要がないのでモデルがない場合(今回はこのパターン)のときであり、ActiveModelの特性をincludeすることでモデルのようなものを作ることができる。

Form Objectを使わない場合、
例えば、コントローラにロジックを記述してファットコントローラーとなったり、独自の作法でフォームを作成するため、ビューとコントローラを両方読まないとどのように動くのか理解できないため、可読性が下がる。

> [Form Objectとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/07_search/index/form_object.md)

# ActiveModelとは?
Active Modelは、Active RecordからDBに依存する部分を除いた振る舞いを提供しているライブラリである。これを利用することにより、DBを利用しないフォームでもActiveRecordを利用したときと同じような記述ができる。


# ActiveModel::Attributesとは?
RubyのクラスにActiveRecordのカラムのような属性を加えられる。
attrbuteをクラスの冒頭に並べると、「クラスが何のパラメータを受けているのか」を明示できるメリットがある。

> [ActiveModel::Attributesを使う - qiita](https://qiita.com/kazutosato/items/91c5c989f98981d06cd4)

# ActiveRecord::Relationとは?
クエリを生成するための情報を保持し、メソッドチェーンでつなげることができるため、再利用性が高い。

> [ActiveRecord::Relationとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/07_search/index/ActiveRecord::relation.md)

# モデルのスコープとは?

- scopeは、関連オブジェクトやモデルへのメソッド呼び出しとして参照される。  

- scopeでは、`where`、`joins`、`includes`などのメソッドを使用できる。  

- どのscopeメソッドも、常にActiveRecord::Relationオブジェクトを返す。

- 単純なscopeを設定するには、クラスの内部でscopeメソッドを使用する。

> [モデルのスコープとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/07_search/index/model_scope.md)

# ルーティングのcollectionとは?
```ruby
resources :posts, shallow: true do
    collection do
      get :search
    end
end
```
GETリクエストと、`posts/search`を認識し、リクエストをPhotosコントローラーのsearchアクションにルーティングする。  
同時に`search_posts_path`や`search_posts_url`ヘルパーも作成される。

> [memberとcollection](https://github.com/Shun712/Knowledges/blob/master/insta_clone/07_search/index/route_member_collection.md)

# 疑問点
- `app/forms/search_posts_form.rb`において、searchアクション内のif修飾子はself(SearchPostsFormのインスタンス)が省略されているのでしょうか?
selfを入れて試しましたが問題ありませんでした。
```ruby
scope = splited_bodies.map { |splited_body| scope.body_contain(splited_body) }.inject { |result, scp| result.or(scp) } if body.present?
    scope = scope.comment_body_contain(comment_body) if comment_body.present?
    scope = scope.username_contain(username) if username.present?
```

- 同じく`app/forms/search_posts_form.rb`において、searchアクション内の`scope = splited_bodies.map { |splited_body| scope.body_contain(splited_body) }.inject { |result, scp| result.or(scp) } if body.present?`部分の解釈は以下でよろしいでしょうか?

[こちらの](https://tech-essentials.work/questions/160)質問を参考にしました。

```ruby
  def search
    scope = Post.distinct
    # mapはブロック内の処理をした結果を配列として返す
    # splited_bodies.map｛ |splited_body| scope.body_contain(splited_body) }
    #  ↓
    # ["電車", "卵", "携帯"].map ｛ |splited_body| scope.body_contain(splited_body) }
    #  ↓
    # [scope.body_contain("電車"), scope.body_contain("卵"), scope.body_contain("携帯")]
    #  ↓
    # これがActiveRecord::Relationの形になっている(配列と形は同じだが、厳密には配列ではない)。例えば、[[a, b, c], [d, e], [f]]。
    #  ↓
    # splited_bodies.map { |splited_body| scope.body_contain(splited_body) }.inject { |result, scp| result.or(scp) }
    #  ↓
    # [scope.body_contain("電車"), scope.body_contain("卵"), scope.body_contain("携帯")].inject { |result, scp| result.or(scp) }
    #  ↓
    # scope.body_contain("電車").or(scope.body_contain("卵")).or.(scope.body_contain("携帯"))
    #  ↓
    # injectメソッドで[a ,b, c, d, e, f]の形にする。
    scope = splited_bodies.map { |splited_body| scope.body_contain(splited_body) }.inject { |result, scp| result.or(scp) } if body.present?
    .
    .
    .
 end

private

def splited_bodies
  body.strip.split(/[[:blank:]]+/)
end
```