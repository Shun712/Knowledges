# deviseでログイン有無のコントローラ設定

deviseのヘルパーメソッドで`authenticate_user!`使い、ユーザーのログイン済みか判断させる。  

# ログインしたユーザーのみアクションが実行できるよう設定

`before_action :authenticate_user!`

# ログインをスキップさせた場合

`skip_before_action :authenticate_user!`

# 参考

[[Rails] authenticate_user! の使い方 - qiita](https://qiita.com/yait/items/c9843157ab633ffa0fe3)

[Devise でログインをスキップする方法](https://k-koh.hatenablog.com/entry/2020/09/13/151128)
