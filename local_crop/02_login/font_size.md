# fontのサイズ変更

## Font Awesomeのサイズの変更

|  コード   |  大きさ  |
|:------:|:-----:|
| fa-xs	 | 0.75倍 |
| fa-lg	 | 1.33倍 |
| fa-2x	 |  2倍   |
| fa-3x	 |  3倍   |
| fa-4x	 |  5倍   |
| fa-5x	 |  7倍   |

`<i class="fab fa-twitter fa-xs"></i>`

### cssを用いてサイズを変更

新しくクラスを作り、そのクラスをCSSで大きさ変更する。

`<i class="fab fa-twitter size"></i>`

```scss
.size{
  font-size:1.5em; /*1.5倍にする*/
}
```

### Font Awesomeの色を変更

`<i class="fab fa-twitter size"></i>`

```scss
.size{
  color:#1da1f2; /*青色にする*/
}
```

# 参考

[Font Awesomeの色とサイズを変える方法 -qiita](https://qiita.com/mzmz__02/items/aaff1d615900cf7d346c)