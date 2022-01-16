# git-flowとは?

プラグイン(ツール)のことである。
[![Image from Gyazo](https://i.gyazo.com/6d6d7e51a54c23d65d7b921bccba5eaa.png)](https://gyazo.com/6d6d7e51a54c23d65d7b921bccba5eaa)

# 各ブランチの役割

1. master
プロダクトとしてリリースするためのブランチ。開発者がmasterブランチのコードを直接修正してコミットすることはない。

2. develop
開発者はこのブランチを起点に**feature**ブランチを切って開発を進め、リリース準備ができたら**master**へマージする。このブランチも開発者が直接修正してコミットすることはない。

3. feature branches
開発者が直接コードを修正してコミットするブランチ。 developから分岐し、**develop**にマージする。
開発の流れ

  - developブランチからfeatureブランチを作成する

  - featureブランチで機能を実装する
  
  - GitHubにプッシュし、developブランチに対してプルリクエストを送る

  - レビューを受けてdevelopブランチにプルリクエストをマージする

developブランチにマージされたらfeatureブランチは不要になるので削除する。

4. hotfix
リリース後のクリティカルなバグフィックスなど、 現在のプロダクトのバージョンに対する変更用のブランチ。 masterから分岐し、 masterにマージし、タグをつける。次にdevelopにマージする。

5. release
developブランチにいくつかのfeatureブランチがマージされ、リリースする準備が整ったら**release**ブランチを作成する。ステージング環境などにデプロイしてみて、そこでバグを修正する。その場合は、**develop**ブランチへマージする。
問題がなければreleaseブランチから**master**ブランチにマージして本番環境にもデプロイする。

# 開発者の流れ

1. featureブランチを切ってコツコツ開発する。
2. プルリクを送り、レビューを受けてdevelopブランチへマージする。
3. featureブランチを削除する
4. リリースする準備が整ったら、releaseブランチを作成しデプロイして問題ないか確認する。
5. 問題があれば修正し、developブランチへマージする。問題がなければ、masterブランチへマージする。

### 参考
[git flowについて](https://github.com/DaichiSaito/insta_clone/wiki/git-flow%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6)
[Git-flowって何？](https://qiita.com/KosukeSone/items/514dd24828b485c69a05)