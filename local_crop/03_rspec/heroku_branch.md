# Herokuにmaster以外のブランチをデプロイ

Herokuでは、**masterブランチ**にpushされたコードがアプリとして実行される。  
開発中(develop)のブランチをHerokuで動作させたい場合は以下のようにpushする。

```
# developブランチをherokuのmasterにpushして動作させる
$ git push heroku develop:master
```

# 参考

[herokuにmaster以外のブランチをデプロイ](https://blog.knjcode.com/push-branch-to-heroku/)

[Herokuへのデプロイ方法](http://judo-engineer.blog.jp/archives/6853624.html)