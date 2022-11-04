[西條学園](https://qiita.com/Vitalize/private/dba4e7112bfc8eb2290c#3-chapter-1-select)

[Chapter 1 SELECT](https://paiza.io/projects/SZG01dpL3Au0y6JfTc2fTg?language=mysql)

[Chapter 2 SELECT sub query, synchronized sub query, JOIN](https://paiza.io/projects/mGFMzEN421sZUej-DhvUyQ?language=mysql)

[Chapter 3 INSERT, UPDATE, DELETE](https://paiza.io/projects/CD0fXZiB6OqyT4FzN3iA_A?language=mysql)

[Chapter 4　実践問題](https://paiza.io/projects/vsNwOWGKXGoQiK3sImR0HQ?language=mysql)

# LIKE

あいまい検索「〇〇〇を含む文字列」を検索する。
- ワイルドカード  
`「%」`ゼロ文字以上の文字列  
`「_」`任意の一文字

- 除外  
`カラム名　NOT LIKE "〇〇%"`

- 複数のあいまい検索  
2つ以上`%`を使える。

```sql
select * from user where name like '%a%a%';
```

## 参考

[【SQL】LIKE句の基本的な使い方～複数検索する場合の方法まで解説 - potepan](https://style.potepan.com/articles/22072.html)

[【SQL】指定の文字列を抽出、除外するLIKE句　複数条件指定も](https://yama-weblog.com/sql-using-like/)

[パターンマッチングを行う(LIKE演算子)](https://www.javadrive.jp/mysql/select/index7.html)

# 数値の整形

- `FORMAT`関数を使用することで、数値を3桁ごとに区切って**整形する**事ができる。

- また、第2引数で小数点以下第何位まで表示することができる。

```
mysql> SELECT FORMAT( 101238777, 2 );
+------------------------+
| FORMAT( 101238777, 2 ) |
+------------------------+
| 101,238,777.00         |
+------------------------+
1 row in set (0.00 sec)
```

## 参考

[数値を整形する (FORMAT) - MySQL関数リファレンス](http://db.yulib.com/mysql/000022.html)

# 文字数を調べる

- `len`関数は、SQLで`文字列のバイト数`を確認する際に使われる関数である。

```
Access：    LEN
SQL Server：LEN
Oracle：    LENGTH
MySQL：     CHAR_LENGTH、CHARACTER_LENGTH
PostgreSQL：LENGTH、CHAR_LENGTH、CHARACTER_LENGTH
```

## 参考

[【SQL】文字数を調べる！SQLでのLENGTH関数の使い方を徹底解説！ - potepan](https://style.potepan.com/articles/22353.html)

[文字列のバイト数を取得する - ギャグ引きSQL構文集](https://www.sql-reference.com/string/octet_length.html)

# AND, ORの複数条件で抽出

カッコで囲むことで優先を付けられる。

```sql
SELECT * 
FROM test_table
WHERE (商品分類 = 'ボトムス' OR 単価 >= 6000) AND 売上金額 >= 100000
```

## 参考

[【SQL超入門講座】13.AND, OR｜複数条件で抽出する方法](https://kino-code.com/sql13/)

# 自己相関サブクエリ

- 外側のクエリの値をサブクエリ内で使用できる。

- サブクエリの`SELECT`文でクエ入りのテーブルの列を参照するものを`サブクエリ`という。

- 自テーブルのと結合した相関サブクエリを`自己相関サブクエリ`という。

```sql
-- 大陸が同じ各国の人口と比べてより大きいか等しいような人口を持つ国をworldから選ぶ 
SELECT continent, name, population 
FROM world x 
WHERE population >= ALL (
 SELECT population 
 FROM world y 
 WHERE y.continent = x.continent 
 AND population > 0 
)
```

## 参考
[https://qiita.com/aki3061/items/736abd6ea883ba647586 - qiita](https://qiita.com/aki3061/items/736abd6ea883ba647586)

[SQLZOOのSELECT within SELECTを解いてみた](https://marucoblog.com/programing/4-select-within-select/)

[相関副問い合わせ(相関サブクエリ)
](https://studydb.gozaru.jp/rsubquery.html)

# COUNT関数

- `WHERE`句内では使えない。`HAVING`を使用する。

- 引数内に3値論理式で条件を指定する。

- 重複を除去したい場合、`COUNT(DISTINCT name)`とする。

```sql
mysql> select count(gender='M' or null) from employees;
+---------------------------+
| count(gender='M' or null) |
+---------------------------+
|                    179973 |
+---------------------------+
1 row in set (0.08 sec)
```

## 参考

[SQLのwhere句でcountが使えない 絞り込み条件に集計関数を使う方法 - potepan](https://style.potepan.com/articles/29682.html)

[SQL distinctとcountを組み合わせてデータ種類をカウントする - potepan](https://style.potepan.com/articles/22701.html)

# AS

- カラム名やテーブル名に別名をつける

- `as`は省略できる。

## 参考

[SQLで別名をつけるならAS句を使いこなそう！つけ方をわかりやすく解説 - potepan](https://style.potepan.com/articles/24708.html)

# UPDATEでデータ更新

- `WHERE`句で複数条件を指定する。

```sql
update employees2 
-- 更新したい値を設定する
set first_name='Tarou', last_name='Yamada' 
-- 対象のレコードを指定する
where emp_no=10001 or ( first_name = 'Kyoichi' and last_name = 'Maliniak' );
```

## 参考

[SQLのupdateでwhere句で更新条件指定 複数条件や別テーブル指定も可 - potepan](https://style.potepan.com/articles/29679.html)

# 3つ以上のテーブル結合

```sql
SELECT
  prodcuts.id, product_i18ns.name 
FROM
  products
JOIN
  product_i18ns
ON
  products.id = product_i18ns.id
RIGHT JOIN
  product_coutries
ON
  products.id = peoduct_coutries.id
WHERE
  locale_id=1 && country_id=233 
```

## 参考

[【SQL】３つ（複数）のテーブルの結合してデータを抽出する - qiita](https://qiita.com/shukan0728/items/d48936928e5ac7aaf7b2)

# GROUP BYで

- 「種類ごとに集計関数を使用する」などといった形で使用する

- `SELECT`句内で指定したカラム名を用いる

- 複数指定できる

```sql
SELECT team, COUNT(team) 
FROM user 
GROUP BY team;
+------------+-------------+
| team       | COUNT(team) |
+------------+-------------+
| チームA    |           3 |
| チームB    |           2 |
+------------+-------------+
```

## 参考

[【MySQL】GROUP BY句に複数のカラムを指定する方法](https://webmaster.chielog.com/sql/155.html)

[【SQL】GROUP BYで自在に集計!集計関数やHAVINGと合わせて使おう](https://www.sejuku.net/blog/72923)

# IN

- 複数の一致するかの条件判定をまとめて行うために使用する命令

- `OR`と同じ

- `IN`をサブクエリとして指定することもある

```sql
SELECT * 
FROM fruit 
WHERE name = "みかん" OR name = "りんご";

SELECT * 
FROM fruit 
WHERE name IN("みかん","りんご");
```

```sql
SELECT 列名1, 列名2, ...
FROM テーブル名
WHERE 列名 IN (
    SELECT 列名
    FROM テーブル名
    [WHERE 条件式など]
)
```

## 参考

[SQLでIN句を使おう!基本からサブクエリ活用方法まで一覧紹介](https://www.sejuku.net/blog/72497)

[IN句を用いた副問合せ](https://www.sql-reference.com/select/subquery_in.html)

# BETWEEN

```sql
SELECT *
FROM test1
WHERE date BETWEEN '2020-07-01 00:00:00' AND '2020-07-31 23:59:59';
```

## 参考

[SQLで日付を範囲指定して抽出条件を絞るやり方！【初心者向け】 - potepan](https://style.potepan.com/articles/24645.html)

# NULL

```sql
SELECT * FROM user WHERE name IS NULL;

SELECT * FROM user WHERE name IS NOT NULL;
```

- `ISNULL`関数は`NULL`の要素に対して、指定した文字列に変換する

```sql
SELECT ISNULL(name, 'UNKNOWN') 
FROM user;
```

## 参考

[【SQL】NULLの上手な扱い方! IS NULL演算子とISNULL関数について](https://www.sejuku.net/blog/72480)
