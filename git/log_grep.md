# ログを確認する

`$ cat tail -f log/development.log | grep -3 "tags"`

- `tail`コマンドでログの最後尾を取り出す。`-f`オプションでファイル指定をする。  

- `grep`コマンドで該当する語句を指定する。

# 参考

[【linux】grepで前後の数行も取得する【コマンド】 - qiita](https://qiita.com/mtanabe/items/a173bc1d78e0d784e115)

[tailコマンドのオプション「f」と「F」 - qiita](https://qiita.com/sakito/items/7f65e16f10b3d754f307)