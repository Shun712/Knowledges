# annotateのスキーマ情報を設定

`annotate`各モデルのスキーマ情報をファイルの先頭もしくは末尾にコメントとして書き出してくれるGemである。

# スキーマ情報をファイルの末尾に書き出してほしい場合

```ruby
- 'position_in_class' => 'before'
+ 'position_in_class' => 'after'
```

# 参考

[【Rails】annotateの使い方 - qiita](https://qiita.com/koki_develop/items/ae6b5f41c18b2872d527#%E3%82%B9%E3%82%AD%E3%83%BC%E3%83%9E%E6%83%85%E5%A0%B1%E3%82%92%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%81%AE%E6%9C%AB%E5%B0%BE%E3%81%AB%E6%9B%B8%E3%81%8D%E5%87%BA%E3%81%97%E3%81%A6%E3%81%BB%E3%81%97%E3%81%84%E5%A0%B4%E5%90%88)