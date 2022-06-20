# Rspecでinvalid session idエラーの解決

`docker-compose`でSeleniumを使ったRspecで、`invalid session id`のエラーが発生した。

# エラー内容

```ruby
Selenium::WebDriver::Error::InvalidSessionIdError:
 invalid session id
```

# 解決方法

メモリ不足が原因だったので、chromeコンテナのメモリを増やした。

```ruby
# docker-compose.yml

chrome:
  image: selenium/standalone-chrome:latest
  shm_size: 256m　　#　←　追加
  ports:
    - 4444:4444
```

shmサイズは、Chromeがコンテンツをダウンロードした際の一時ファイル領域のこと。

# 参考

[docker-composeでSeleniumを使ったRspecでinvalid session idエラーの解決方法 - qiita](https://qiita.com/na-tsune/items/fed1919432c0392a3b29)