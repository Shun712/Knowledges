# 10 通知機能の実装

# やったこと
- 通知機能を実装してください。

- タイミングと文言は以下の通りとします。（リンク）と書いてある箇所はリンクを付与してください。


- フォローされたとき

    - xxx（リンク）があなたをフォローしました

    - 通知そのものに対してはxxxへのリンクを張る

- 自分の投稿にいいねがあったとき

    - xxx（リンク）があなたの投稿（リンク）にいいねしました

    - 通知そのものに対しては投稿へのリンクを張る

- 自分の投稿にコメントがあったとき

    - xxx（リンク）があなたの投稿（リンク）にコメント（リンク）しました

    - 通知そのものに対してはコメントへのリンクを張る（厳密には投稿ページに遷移し当該コメント部分にページ内ジャンプするイメージ）

- 既読判定も行ってください。通知一覧において、既読のものは薄暗い背景で、未読のものは白い背景で表示しましょう。

- 既読とするタイミングは各通知そのものをクリックした時とします。

- 不自然ではありますが通知の元となったリソースが削除された際には通知自体も削除する仕様とします。

# ポリモーフィック関連とは?
特定の親モデルを持たずに、いろいろな親モデルを持つことができる関連付けの仕組みをポリモーフィックと呼ぶ。また、ポリモーフィックはダックタイピングの一つでオブジェクト指向を実現する方法である。

> [ポリモーフィック関連とは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/10_notification/index/polymophic.md)

# enumとは?
1つのカラムに指定した複数個の定数を保存できるようにするためのモノである。
このenumを使用すると指定した複数個の定数以外は保存できなくなる。  
また、カラムに指定した定数が入っているレコードを取り出すのが容易になる。

> [enumとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/10_notification/index/enum.md)

# URLヘルパーとは?
URLヘルパーが使われるのは、Webリクエストのコンテキスト、つまり**ビューやコントローラーの中**である。  
この場合は、リクエストの`host`やドメインは**アプリケーションが自動的**に提供する。  
ビューやコントローラーの外では、`_url`や`_path`で終わるヘルパーに`host`を明示的に提供する必要がある。

> [URLヘルパーとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/10_notification/index/url_helper.md)
>
# lメソッドとは?
```azure
Tue, 30 Jul 2020 00:12:12 +0000
```

日本人には見慣れない、時刻表示を見慣れた表示にする。

```azure
2020/02/10 09:12:12
```

(config/locales/ja.yml)
```yaml  
  time:
    formats:
      default: "%Y年%m月%d日(%a) %H時%M分%S秒 %z"
      long: "%Y/%m/%d %H:%M"
      short: "%m/%d %H:%M"
```

formatsオプションを付けると、書式を切り替えることができる。

# 詰まったこと
ヘッダーの通知を表示させる際、dropdownが機能していなかったので`popper.js`をCDNで読み込ませてバグを修正した。
[こちら](https://tech-essentials.work/questions/376)を参考にした。

# 疑問点
```ruby
class Comment < ApplicationRecord

  has_one :activity, as: :subject, dependent: :destroy
  after_create_commit :create_activities

  private

  def create_activities
    Activity.create(subject: self, user: post.user, action_type: :commented_to_own_post)
  end
end
```
```
# Table name: activities
#
#  id           :bigint           not null, primary key
#  action_type  :integer          not null
#  read         :boolean          default(FALSE), not null
#  subject_type :string(255)
#  created_at   :datetime         not null
#  updated_at   :datetime         not null
#  subject_id   :bigint
#  user_id      :bigint
#
# Indexes
#
#  index_activities_on_subject_type_and_subject_id  (subject_type,subject_id)
#  index_activities_on_user_id                      (user_id)
#
# Foreign Keys
#
#  fk_rails_...  (user_id => users.id)
```

`app/models/comment.rb`や`app/models/like.rb`、`app/models/relationship.rb`内で共通するcreate_activitiesアクションにおいて、  
コメント、いいね、フォローのいずれかをした際にActivityオブジェクトを生成していますが、この時の属性について疑問があります。

Activitiesテーブルには、`subject_id`と`subject_type`がポリモーフィックオプションによって生成されましたが、  
`Activity.create(subject: self, user: post.user, action_type: :commented_to_own_post)`でカラムにないsubject属性だけで、なぜ  
`subject_id`と`subject_type`のレコードが保存されるのでしょうか？  
また、user属性についても同様です(userで`user_id`が保存される)。
クエリを確認してみると、
```
Activity Create (3.7ms)  INSERT INTO `activities` (`subject_type`, `subject_id`, `user_id`, `action_type`, `created_at`, `updated_at`) VALUES ('Comment', 10, 25, 0, '2022-02-10 21:57:01', '2022-02-10 21:57:01')
```
となっており、`subject_id`と`subject_type`がDBに保存されており挙動に疑問を持ちました。  
愚直に、  
`Activity.create(subject_id: self.id, subject_type: self.class, user: post.user, action_type: :commented_to_own_post)`
もできるなと思いました(問題なく動きました)。