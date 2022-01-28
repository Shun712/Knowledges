# uniqueness: scope を使ったユニーク制約方法
`uniqueness: scope`を実装するとユニーク制約をできる。  
以下はコンソールで試したことである。
```
[1] pry(main)> post = Post.first

# post に user_id:1 が「いいね」する
[2] pry(main)> post.likes.create(user_id: 1)

   (5.1ms)  COMMIT
 
 # 再び、post に user_id:1 が「いいね」するとロールバックされる
[3] pry(main)> post.likes.create(user_id: 1)

   (0.2ms)  ROLLBACK
 
 # post に user_id:2 が「いいね」する
[4] pry(main)> post.likes.create(user_id: 2)

   (1.4ms)  COMMIT

```