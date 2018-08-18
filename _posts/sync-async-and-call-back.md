Promise



答應我，你會回來。





Promise是爲了解決callback hell而誕生的。



其實我對callback一直有一種一知半解的模糊感，所以藉由這次機會。決定好好的認識一下它。



要瞭解callback.就得先認識同步sync跟異步async的概念，先不要害怕，一下子又是promise, 一下子是callback, 一下子是sync, async, 但我們先區分清楚要解決的問題是什麼，再來瞭解這些名詞。



但~~~還有個最最基本的javascript特性要認識，那就是javascript是個single thread的語言，這表示，你只有一個process可以來處理你寫的程式碼，怎麼處理呢？就是依序執行你的程式碼，從第一行到最後一行。

上面其實就是同步。依序的執行程式碼。很像去ktv點歌，大家都乖乖的，沒有人插播。



像下面範例。

```
let a = 5;
let b = 6;

let doubleNumber = function(num){
    return number*2;
};

let tripleNumber = function(num){
    return number*3
};

console.log( doubleNumber( a ) ); 


```



但有一種情況，你可能需要插播。

就是你不知道什麼時候會處理完某一塊的程式碼，但你又不想浪費時間等待。

這好像原本輪到他唱歌的人去上廁所了，不知道什麼時候會上完，所以原本他點的歌就先凍結，等到他回來的時候在插播。

所以上面這種，**有不知道什麼時候會回來，但又不想浪費時間等待的**，就叫做異步處理。



再看另外一個用在web上常見的例子，比方說我們向伺服器發送一個請求，要跟他要點資訊，但是因爲網路的關係不知道什麼時候伺服器會把東西丟回來，但我們又不能讓使用者乾等，可能要顯示loading的狀態，等到請求回來的時候，再去把資訊顯示出來。



注意了，這個等到請求回來的時候，再去做某些事的這個某些事，就是callback function。有些人會翻譯成回調，是回來再調用Function的意思。但也可以想成這個call, 回來(back)時，要去做的事。



像setTimeout就是最簡單的callback function example。現在不要處理，等到n秒後再處理。



```

let a = 5;

setTimeout( function(){ a++; }, 1000 );

console.log( a );

```



像上面的執行結果執行到setTimeout時，等於通知javascript engine有人要去上廁所了，先播下一首歌，等到1秒後那個人回來，再插播他的歌。

像這樣。

```
5
6 // 一秒後印出。
```



那promise呢？



請待續。



