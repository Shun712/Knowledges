# APIアプリケーションについて

`--api`というオプションをつけることでAPIモードを意味する。

```ruby
$ rails new uber-eats-like --api
  create
  create  README.md
  create  Rakefile
  create  .ruby-version
  create  config.ru
  create  .gitignore
  create  Gemfile
  ...
  Using spring-watcher-listen 2.0.1
  Using sqlite3 1.4.2
  Bundle complete! 9 Gemfile dependencies, 54 gems now installed.
  Use `bundle info [gemname]` to see where a bundled gem is installed.
           run  bundle binstubs bundler
  The dependency tzinfo-data (>= 0) will be unused by any of the platforms Bundler is installing for. Bundler is installing for ruby but the dependency is only for x86-mingw32, x86-mswin32, x64-mingw32, java. To add those platforms to the bundle, run `bundle lock --add-platform x86-mingw32 x86-mswin32 x64-mingw32 java`.
          run  bundle exec spring binstub --all
  * bin/rake: Spring inserted
  * bin/rails: Spring inserted
```

# Reactプロジェクトを作成

[![Image from Gyazo](https://i.gyazo.com/8d49410b96ade26cc042c45fb9abae4c.png)](https://gyazo.com/8d49410b96ade26cc042c45fb9abae4c)

Railsのサーバーサイドは`app/...`のディレクトリに、Reactは`frontend/`のディレクトリにコードを書いていく。  
`localhost:3000` のAPIサーバーに対して、フロントエンドは`localhost:3001`で動かすと、両者が疎通する。

```
# frontendという名前でReactアプリケーションを構築する。
# frontendディレクトリで下記コマンドを実行する。

$ npx create-react-app frontend
```

コマンドを実行すると以下のディレクトリやファイルが生成される。

[![Image from Gyazo](https://i.gyazo.com/b53b29628addcc3ac06891d595e30236.png)](https://gyazo.com/b53b29628addcc3ac06891d595e30236)
