# Github Actionsにwebpackerを導入

Github Actionsには、webpackerが導入されていないので、RSpecを実行中に  

```ruby
Webpacker::Manifest::MissingEntryError: Webpacker can't find application in /app/public/packs/manifest.json. Possible causes:
1. You want to set webpacker.yml value of compile to true for your environment
unless you are using the `webpack -w` or the webpack-dev-server.
2. webpack has not yet re-run to reflect updates.
3. You have misconfigured Webpacker's config/webpacker.yml file.
4. Your webpack configuration is not creating a manifest.
```
というエラーが発生しする。

# Webpackerのインストール

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
    steps:
      - uses: actions/checkout@v2
      - name: Install chrome
        run: |
          wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add -
          echo 'deb http://dl.google.com/linux/chrome/deb/ stable main' | tee /etc/apt/sources.list.d/google-chrome.list
          apt update -y
          apt install -y google-chrome-stable libvips
      - name: bundler config
        run: bundle config set path 'vendor/bundle'
      - name: cache gems
        id: cache-gems
        uses: actions/cache@v2
        with:
          path: vendor/bundle
          key: ${{ runner.os }}-gems-${{ hashFiles('**/Gemfile.lock') }}
          restore-keys: |
            ${{ runner.os }}-gems-
      - name: install node
        run: |
          curl -sL https://deb.nodesource.com/setup_12.x | bash -
          apt-get install -y nodejs
      - name: install yarn
        run: |
          curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
          echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
          apt-get update
          apt-get install -y yarn
      - name: setup bundle
        if: steps.cache-gems.outputs.cache-hit != 'true'
        run: |
          bundle install --jobs 4 --retry 3
      - name: setup db schema
        run: |
          bundle exec rails db:create db:schema:load --trace

      # 以下でWebpackerを導入
      - name: Webpack compilation
        run: |
          bundle exec rails webpacker:install
          bundle exec rails webpacker:compile

      - name: run spec
        run: bundle exec rspec spec/models
      - name: Archive rspec result screenshots
        if: failure()
        uses: actions/upload-artifact@v3
        with:
          name: rspec result screenshots
          path: |
            tmp/screenshots/
            tmp/capybara/
```

# 参考

[circleciでrspecを実行すると、Webpacker can't find applicationのエラーが出た - qiita](https://qiita.com/ashketcham/items/6ce1d0b5a46f177cf32a)

[Unable to build Rails with Webpack on Github Actions](https://stackoverflow.com/questions/58799342/unable-to-build-rails-with-webpack-on-github-actions)