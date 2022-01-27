# Ajax(非同期通信)

> AjaxはもともとAsynchronous JavaScript + XMLの略で、Webブラウザ上で動作するJavaScriptでサーバからXMLデータを取得し、取得したデータをコンテンツに動的に反映するという手法

# 同期通信の場合

webブラウザからサーバーにリクエストを通信し、レスポンスが戻ってくる。  
この時、すべての情報を通信しているので、一瞬画面が白くなる。  
つまり、**サーバーからレスポンスが返ってくるまで、他の作業ができない。**

# 非同期通信の場合

webブラウザから一部の情報をリクエストするので、それ以外の部分が変わらず、画面が白くならない。
つまり、**サーバーからレスポンスが返ってこなくても他の作業ができる。**

[![Image from Gyazo](https://i.gyazo.com/0bbd72d8eb5206fa047ffd05be99ebe1.png)](https://gyazo.com/0bbd72d8eb5206fa047ffd05be99ebe1)

> [非同期通信Ajaxをできるだけ分かりやすく説明してみた](https://applingo.tokyo/article/654)

# XMLHttpRequest

> クライアントとサーバーの間でデータを伝送するための機能をクライアント側で提供する API です。
> ページ全体を再読み込みすることなく、URLからデータを読み出す簡単な方法を提供します。
> このAPIによって、ユーザの作業を中断させることなくWebページの一部を更新することができます。
> (MDNより)

要するに、ブラウザ上でサーバーとHTTP通信を行うためのAPIである。
このAPIを使って実装するのが、JavaScriptである。

# JavaScript

XMLHttpRequestはJavaScriptの組み込みオブジェクトである。  
組み込みオブジェクトとは、あらかじめ定義されているオブジェクトのことである。

# DOM

> Document Object Model (DOM) は、HTML および XML ドキュメントのための API です。これはドキュメントの構造的な表現を提供し、内容や表示形態の変更を可能にします。端的に言えば、Web ページをスクリプトやプログラミング言語とつなぐような機構です。
> (MDNより）

Ajaxを使って、動的なWebページを作成するときに、HTML・XML上のどの要素を変更するかを指定する。そこでDOMはHTMLやXMLを「ツリー構造」として展開し、アプリケーション側に文章の情報を伝え、加工や変更をしやすくする。

# 参考
[初心者目線でAjaxの説明 - qiita](https://qiita.com/hisamura333/items/e3ea6ae549eb09b7efb9)

[非同期通信Ajaxをできるだけ分かりやすく説明してみた](https://applingo.tokyo/article/654)