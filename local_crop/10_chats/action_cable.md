# HTTP通信

[![Image from Gyazo](https://i.gyazo.com/36ed5a8417dd8944766dbadd919669f8.png)](https://gyazo.com/36ed5a8417dd8944766dbadd919669f8)

HTTP通信とは、WebブラウザとWebサーバー間でHTMLや画像ファイなどの送受信に用いられる通信プロトコルである。
**しかし、HTTP通信はサーバーにリクエストが送られない限り、情報は更新されない。**

# Ajax通信

[![Image from Gyazo](https://i.gyazo.com/f4d1ce456de79bacdd1543e75a245b8f.png)](https://gyazo.com/f4d1ce456de79bacdd1543e75a245b8f)

Ajax通信とは、Javascriptを使って非同期でサーバーとやり取りすることである。JavaScriptが通信を行うため、ページ遷移を行わずに情報の更新をすることができる。
**Ajax通信は裏でリクエストを送ってJavascriptで書き換えるだけで、リアルタイムなやり取りは常に裏でやり取りしなければならない。**

# WebSocket通信(ActionCable)

[![Image from Gyazo](https://i.gyazo.com/aca9064fb3d274f2634fe6eed77cdcaa.png)](https://gyazo.com/aca9064fb3d274f2634fe6eed77cdcaa)

WebSocket通信とは、サーバー側とユーザー側を常時接続状態にしておき、双方向通信できる仕組みである。クライアントがリクエストを送信せずに、リアルタイムで情報を更新できる。

# 参考

[【Rails6.0】ActionCableを使用したライブチャットアプリを実装する手順を解説](https://techtechmedia.com/action-cable-rails6/)

[Feature/direct messages -github](https://github.com/DaichiSaito/insta_clone/pull/37/files)

[Action Cable の概要 - Railsガイド](https://railsguides.jp/action_cable_overview.html)

[【Rails6.0】ActionCableとDeviseの欲張りセットでリアルタイムチャット作成(改正版) - qiita](https://qiita.com/rhiroe/items/4c4e983e34a44c5ace27)

[【Rails】非同期通信でチャット/DM機能を実装する - qiita](https://qiita.com/mi-1109/items/660ec3630e76f11d1f16)

[[Rails]ActionCableを使用してリアルタイムチャットの実装 - qiita](https://qiita.com/bty__/items/249c93970780b498d86e#rooms_controller)

[【Rails】Action Cableで非同期なチャット機能を実装する方法](https://pote-chil.com/rails_chat-line/)

[【Rails6】（送信時のリロード無し！）Action CableでSlack風チャットアプリを作成 - qiita](https://qiita.com/take18k_tech/items/00cc14c0eff45073ffc7#4-0-%E6%BA%96%E5%82%99)