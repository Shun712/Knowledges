# タイムゾーンを考慮するDate

`Date.now`や`Date.today`だと時間軸がサーバーのものに適用されるので、`current`メソッドを使ってタイムゾーンを設定した時間軸に適用させる。

# 参考

[14 Dateの拡張 - railsガイド](https://railsguides.jp/active_support_core_extensions.html#date%E3%81%AE%E6%8B%A1%E5%BC%B5)