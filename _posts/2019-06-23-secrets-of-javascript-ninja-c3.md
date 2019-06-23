---
layout: post
title: "Secrets of Javascript NinJa - C3 - First class functions for the novice: definitions and arguments"
description: "介紹函式作爲第一公民的特性跟優點"
date: 2019-06-23
tags: [js, reading]
comments: true
share: true
---
C3 - First class functions for the novice: definitions and arguments
---



函式是第一公民(Function as first class citizen)的意思，簡單來說就是其他角色可以做的，函式也可以做。利用函式是第一公民的身份，可以把它當成變數傳遞，跟有其他功能，像是下面這些。

- 可以 `Created via literals`
- 可以被賦值給變數或屬性
- 可以以參數方式傳遞
- 可以被當成結果回傳回去
- 是一個物件，可以有方法跟屬性。


下面的範例針對如何儲存函數，比方說如果需要管理某個事件發生後所需要的`callback`，可以檢查傳進來的`callback`是否已經存在過，如果存在，可以直接呼叫。

```
var store = {
  nextId: 1,
  cache: {},
  add: function(fn) {
    if (!fn.id) {
      fn.id = this.nextId++;
      this.cache[fn.id] = fn;
      return true;
    }
  }
};

function ninja() {
  console.assert(store.add(ninja), "Function was safely added.");
  console.assert(!store.add(ninja), "But it was added once.");
}
```

這個策略比較像是如何檢查陣列中沒有重複的數字的難題，當然可以每次要檢查的時候都遍歷一次整個陣列，可是這個方法的時間複雜度就是$O(n$), 可以善用`Map`來完成這件事，只要記得這個函數是不是存在這個`Map`即可。

上面的用法是讓以變數方式傳進來的函數設定而外的值，之後檢查這個值即可。




### Memoization 

這個構造函數處理的過程，可以記得上次的結果，比方說如果是一個檢查是不是質數的函數，就可以用這種方法實現。先爲這個函數設定一個儲存的空間，然後再把結果存到這個空間去。


```
function isPrime(value) {
  if (!isPrime.answers) {
    isPrime.answers = {};
  }
  if (isPrime.answers[value] !== undefined) {
    return isPrime.answers[value];
  }
  var prime = value !== 0 && value !== 1;
  for (var i = 2; i < value; i++) {
    if (value % i === 0) {
      prime = false;
    }
  }
  return (isPrime.answers[value] = prime);
}

console.assert(isPrime(5), "5 is prime!");
console.assert(isPrime.answers[5], "the answer should be cached");
```



典型的用空間換取時間，爲了效能好一點，就存多點之後需要用到的資訊。

這個方法的兩個好處是

1. 節省時間，如果已經存在答案，就直接回傳答案
2. 不需要重新發送請求, 暫存資訊 (Cache)。



### 四種函式類型

1. function declarations and function expression

   `function declarations` 以 `function` 爲開頭，必須要有函式名稱，一個函式的基本要求是要能夠被呼叫。

   ```javascript
   // 用名字+()來調用函式, myFunc()
   function myFunc() {
   	return 1
   }
   
   // 用變數名字+()來調用函式, myfuncExpression()
   var myfuncExpression = function() {
   	console.log(myfun)
   }
    
   // 因爲是匿名函式，所以爲了讓js解析時知道需要馬上執行，因此用()
   // 內放function(){}的方式來invoke
   // 如果是function(){},解析時會儲存function(){}，而不會馬上invoke
   (function(){
   	console.log("IFFE")
   })()
   
   //另一種立即調用的方法
   (function(){ console.log("abc")}())
   ```

2. 箭頭函式

	```javascript
   // param => expression
   let myFunc = x => x * 2 
   ```

3. 構造函式

    ```javascript
    new Function('a', 'b', 'return a + b')
    ```


4. 生成器函式

   ```javascript
   function *myGen() {
   	yield 1;
   }
   ```



#### Parameter v.s Argument

> Parameter, 定義函式時在()內的變數名稱
> arguemnt, 調用函式時傳遞給函式的值。

如果 `argument` 數量 >` parameter` 的數量，多餘的 `argument` 不會被賦值，如果`parameter` 的數量大於 `argument` 的數量，那多餘的 `parameter` 的值預設是`undefined`，現在以支援對parameter設定預設值。

```javascript
/* x, y 都是 parameter
 * parmas { number } x 
 * parmas { number } y
 */
function add(x, y) {
	return x + y;
}

// 這裏的5, 6是argument
add (5, 6); 

// argument 數量 > parameter的數量
function add(x, ...y){
  console.log(x);
	console.log(y);
}

add(1, 2, 3, 4);  // 1,  [2, 3, 4]

// parameter的數量大於argument的數量
function abc(x, y, z, e, g){
	console.log(x, y, z, e, g)
}

let a = [1, 2, 3];
abc(...a); // 1, 2, 3, undefined, undefined

// 爲 parameter 設定預設值
function add(x=0, y = 0){
	return x + y;
}
add(); // 0

```



### 總結

1. 擅用函式其實也可以有自己的屬性跟方法，我們可以擅用這些來儲存資訊。像是用它來做`cache`之類的。
2. 擅用函式是第一公民的特性優點


