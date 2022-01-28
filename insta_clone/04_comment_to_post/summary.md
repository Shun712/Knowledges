## やったこと

- 編集・更新はモーダルを表示させ非同期で行う。form_withを利用すること。

- 文字列長など適切なバリデーションを付与する

- shallowルーティングを使用する

## Ajaxとは?
 > AjaxはもともとAsynchronous JavaScript + XMLの略で、Webブラウザ上で動作するJavaScriptでサーバからXMLデータを取得し、取得したデータをコンテンツに動的に反映するという手法
 
 Ajaxは非同期通信を用いており、webブラウザから一部の情報をリクエストするので、それ以外の部分が変わらず、画面が白くならない。
つまり、**サーバーからレスポンスが返ってこなくても他の作業ができる。**

[![Image from Gyazo](https://i.gyazo.com/0bbd72d8eb5206fa047ffd05be99ebe1.png)](https://gyazo.com/0bbd72d8eb5206fa047ffd05be99ebe1)

> [Ajaxとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/04_comment_to_post/index/ajax.md)
 
## モーダルとは?

指定された操作を完了するかキャンセルするまで、他のウィンドウを開くことができないウィンドウのこと。

[![Image from Gyazo](https://i.gyazo.com/fb14563757cb443c0ef16356091c84bd.png)](https://gyazo.com/fb14563757cb443c0ef16356091c84bd)

モーダルの役割は、ユーザーにウェブサイトやアプリケーションの運営者が望んだ操作を強制できることである。

> [モーダルとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/04_comment_to_post/index/modal.md)

## prepend()とは?
指定の要素内に文字列やHTML要素を追加することができるメソッドである。

>[prepend()とは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/04_comment_to_post/index/prepend.md)

## form_withの利用

`form_with`は渡されたものによって、行うHTTPメソッドとアクションをそれぞれ判断してくれる。
`form_with model: [post, comment]`のように複数モデルを受け取ると、  
例えば、1つ目のpostが中身あり、2つ目のcommentが中身なしということで、それぞれから`posts/:id/comments`というパスを自動で判断し、さらに中身なしということで`comment_controller.rb`のcreateを呼び出す。

> [form_with](https://github.com/Shun712/Knowledges/blob/master/insta_clone/04_comment_to_post/index/form_with.md)

## shallowルーティングとは?
`shallow`は、ネストしたルーティングにおいて、下層にあるテーブルのIDが一意なら、その上にあるテーブルのIDは不要というメリットである。
つまり、`index`、`new`、`create`アクションについては、どのpostのidに紐づくか示さないと一意に保つことができない。
一方、`edit`、`update`、`destroy`アクションについては、postのidがなくても、commentのidでどのコメントか明らかになる。

> [shalloとは?](https://github.com/Shun712/Knowledges/blob/master/insta_clone/04_comment_to_post/index/shallow.md)