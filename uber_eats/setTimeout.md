# setTimeoutの使い方

`setTimeout(処理内容,実行タイミング)`

setTimeoutは、第二引数に与えられた実行タイミング(ミリ秒)で、第一引数に定義された処理内容を1度実行する。

```javascript
var alertmsg = function(){
  alert("3秒経過");
}
setTimeout(alertmsg, 3000);
```

上の例だと、alertmsg変数にセットされた関数(処理内容)が3秒遅れて実行される。

# clearTimeoutでタイマーを停止する

```javascript
var id = setTimeout(関数, ミリ秒);
 
clearTimeout(id);
```

```javascript
var alertmsg = function(){
  alert("3秒経過");
}
 
var id = setTimeout(alertmsg, 3000);
 
clearTimeout(id);
```

一番最後に`clearTimeout()`を実行し、3秒経過しても「`alertmsg()`」は実行されずに停止する。

# クリックしたら順番に表示

```javascript
<input type="button" value="Check" onclick="myfunc()">
 
<script>
var alertmsg = function(){
  alert("5秒経過");
}
 
var myfunc = function(){
setTimeout(alertmsg, 5000);
}
</script>
```

# setTimeoutが動作しないパターン

```javascript
function hello(name) {
  console.log('Hello,' + name);
}
  
setTimeout(hello('Taro'), 2000);
```

`setTimeout()`の第1引数に( )を付与すると**即時に実行**されてしまう。

```javascript
function hello(name) {
  console.log('Hello,' + name);
}
  
setTimeout(hello, 2000, 'Taro');
```

setTImeout()メソッドには**第3引数**が存在しており、ここに引数となる値を設定することができる

# 参考

[【JavaScript入門】setTimeoutの使い方とサンプル事例まとめ！](https://www.sejuku.net/blog/24540)