# Promiseとは?

- PromiseとはJavaScriptにおいて、非同期処理の操作が完了したときに結果を返すものである。  

- Promiseは処理が実行中の処理を監視し、処理が完了すれば`resolve`、反対に問題があれば`reject`を呼び出してメッセージを表示する。

# コールバックとは

- ある関数Aへ別の関数Bを渡すことである。

```javascript
関数A(関数B、引数) {
    //実行内容
}
```

- コールバックは使い勝手がいい反面、使いすぎるとコードが非常に読みにくくなる欠点がある。

### 非同期処理のコールバック例

javascriptは非同期処理のコールバック関数地獄はネストが深くなるので、**それを防ぐのがPromise**である。

```javascript
sampleFunction1(function(data1) {

    sampleFunction2(function(data2) {
        
        sampleFunction3(function(data3) {
            
            sampleFunction4(function(data4) {
                //処理
            });
            
        });
        
    });
    
});
```

# Promiseの使い方

```javascript
new Promise(function(resolve, reject) {
    resolve('成功');
});

new Promise(function(resolve, reject) {
    reject('失敗');
});
```

### thenを使ってコールバックを処理を実行

```javascript
var sample = new Promise(function(resolve, reject) {
    setTimeout(function() {
        resolve();
    }, 1000);
});

sample.then(function(value) {
    console.log("Promise成功!");
});

console.log("先に出力");
```

`promise.thenを`実行すると、処理した結果の"Promise成功！"という文字列が`result`に引き渡されます。そのため`console.log`で`result`を表示すると、"Promise成功！"という文字がコンソール上に表示されます。

[![Image from Gyazo](https://i.gyazo.com/28639fd2aeca22bee2329dd40b86aab5.png)](https://gyazo.com/28639fd2aeca22bee2329dd40b86aab5)

# 参考

[はじめてのPromise - qiita](https://qiita.com/doidoidon/items/fdc32896319f487993f3)

[【JavaScript】初心者にもわかるPromiseの使い方](https://techplay.jp/column/581)

[Promise、async/awaitに立ち向かう - qiita](https://qiita.com/papi_tokei/items/265d11dd385d053526e2)