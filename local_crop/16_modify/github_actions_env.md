# Github　Actionsで環境変数を設定

ymlファイルに書きたくないAPIキーなどをGithub ActionsのJobで使いたいときの方法

# job定義ファイルで環境変数を使用する

```yaml
name: Test
on: [push]
jobs:
  rspec:
    runs-on: ubuntu-latest
    services:
      db:
        image: mysql:5.7.38
        ports:
          - 3306:3306
        env:
          TZ: "Asia/Tokyo"
          MYSQL_ROOT_PASSWORD: mysql
        options: --health-cmd="mysqladmin ping -pmysql" --health-interval=5s --health-timeout=2s --health-retries=3
    container:
      image: ruby:2.7.5
    env:
      RAILS_ENV: test
      GMAIL_ADDRESS: ${{ secrets.GMAIL_ADDRESS}}
```

### 変数をGithubの設定に追加

[![Image from Gyazo](https://i.gyazo.com/c7395de44ed1d58d4fc58275d5408906.png)](https://gyazo.com/c7395de44ed1d58d4fc58275d5408906)

# 参考

[github actionの環境変数について - qiita](https://qiita.com/daigo01090118/questions/3d7cbe3d5459e7a6eb0e)

[【Github Actions】独自の環境変数設定方法 - qiita](https://qiita.com/sayama0402/items/f019cac4bcb7d420505a)