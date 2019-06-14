---
layout: post
title: "Secrets of Javascript NinJa - C2"
description: ""
date: 2019-06-14
tags: [js, reading]
comments: true
share: true
---
Study notes for Secrets of Javascript Ninja
---



# C1

## 1.3 Using current best practice
### Debugging

列出各瀏覽器下的各種`Debug`工具
像是 `Firefox` 的` Firebug or Chrome` 的 `dev-tool` 等

### Testing
可以用`assert`來做測試

```js
// condition example: expected === actual
assert(condition, message);

```
### Performance
測試一段代碼的 `performance`
```js
console.time("operation_name");

for(let i = 0; i < maxCount; i++){
  // your code here
}

// need to be the same operation
console.timeEnd("operation_name");

```

最後會得到這樣的結果

```
operation_name: 854.980224609375ms
```

爲了得到更精確的效能數據，其實可以多跑幾次，得到合理值。





# C2

## The life cycle overview
1. 使用者輸入網址(`URL`)
2. 瀏覽器產生請求給伺服器
3. 伺服器執行收到請求，產生相對應的Response給client
4. 瀏覽器開始處理`HTML, CSS, Javascript`並開始建構頁面結果 (page building)
5. 產生 `event queue`,一次處理其中一個事件
6. 使用者操作頁面
7. 瀏覽器負責事件處理知道使用者把網頁關掉



![image-20190614115456586](./images/image-20190614115456586.png)



## The page building phase



`HTML`只是瀏覽器拿來建構`DOM`的藍圖而已，瀏覽器拿到`HTML`後，開始照著上面的程式碼, 一個一個建立節點，最上面的是`HTML`，每個節點都可以有很多子節點。

下圖是建立的對照圖。

![image-20190614115937301](./images/image-20190614115937301.png)



既然`HTML`只是藍圖，最後還是會由瀏覽器來解析並創建`DOM`， 藍圖還是有可能會出錯，當出錯的時候，聰明的瀏覽器也會自動幫忙更正。





## Executing Javascript code
在`Script`這個元素內的`Js Code`會讓`browser`的`js engine`執行。
瀏覽器提供的全域變數，就是`window`這個物件，`browser API`可以透過這個來取得，在`window`下最重要的就是`document`這個`object`，它代表這頁`DOM`，所以可以透過`Javascript`來操作這個`document`的物件來改變`DOM`。


#### Global code and function

```
<script>
// function code
  function write(str){
    console.log(str);
  }

// global code
  var first = document.getElementById("first");
  write("something");
</script>
```

當瀏覽器在創建`DOM`階段時，解析到`script tag`內的`global code`，此時`javascript engine`會立即執行這段程式碼，而暫停建立`DOM`，一直到執行到最後一行`Javascript`執行完畢，才會繼續建造節點。只要有還沒處理完的`HTML`元素，當還有還沒有執行完的`Javascript`, 這兩個下列兩個步驟會交替進行。

1. Construct HTML to DOM
2. Execute Javascript Code



## Event handling

瀏覽器的執行環境一次只執行一段程式碼, 是 `single-threaded execution model`。

用櫃檯做比喻，櫃檯一次只處理一個客戶所帶來的任務，其他人都要排隊。因爲客人不總是會耐心等候，所以需要一種方式來追蹤已經領號碼牌但是還沒被處理的客人。`Javascript`用`event queue`來處理這個事件。

所有已經發生的事件，像是滑鼠或鍵盤事件，或其他用戶產生的事件,都會以瀏覽器偵測到事件的順序排序到事件列中。

1. 瀏覽器看 `event queue` 的第一個事件
2. 如果沒有事件，瀏覽器持續偵測
3. 如果有事件, 且已經有註冊的`event handler`, 瀏覽器會執行這個`handler`, 執行`handler`的時候其他事件就繼續等著被處理。
   

因爲一次只有一個事件被處理，所以如果`handler`需要花很多時間執行，就有可能造成`block`現象。



### Event是非同步的

總共有這幾種事件
1. Browser events, like page load...
2. Network events, like response coming...
3. User events, like mouse click ...
4. Timer events, like timeout expires...



### Event Handler

有兩種註冊事件的方式，
1. 把事件發生時要呼叫的` function Assign` 給某些` property `。書中不建議這個方式，因爲全域變數的關係，指派的函式容易被複寫。

  ```js
  window.onload = () => {
    // do something here
  }
  ```
2. 用 addEventListener 來註冊

```html
<ul id="second"></ul>
<script>
 document.body.addEventListener('mousemove', function(){
   let second = document.getElementById("second");
   addMessage(second, "Event: mousemove");
 })
</script>
```