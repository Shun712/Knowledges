# git rebaseの使い方

1. 他ブランチのコミットを吸収して、ログを整理する。

[![Image from Gyazo](https://i.gyazo.com/871b691f7561f31eb4e4c166d4c401ec.png)](https://gyazo.com/871b691f7561f31eb4e4c166d4c401ec)

`git rebase [つなぐ元にするブランチ名]`

2. 同ブランチ内のコミットを1つにまとめる

[![Image from Gyazo](https://i.gyazo.com/1c545676c26f3b257c511e5a85e568a8.png)](https://gyazo.com/1c545676c26f3b257c511e5a85e568a8)

`git rebase -i [開始地点のコミットID]`

統合するコミットのpick(何もしない)部分をsquash(統合する)に変更する。ただし、先頭はpickのままにする。

```
pick d9a1f0e コミットA
squash 400f340 コミットB
squash f35185d コミットC
squash 8dfc486 コミットD
```

# mergeとの違い

- rebaseはまだpushしていないもの

- mergeはすでにpushしているもの

# 参考

[これで完璧! 図解でわかるgit rebaseの2つの使い方!](https://www.sejuku.net/blog/71919