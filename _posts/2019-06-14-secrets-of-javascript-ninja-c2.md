---
layout: post
title: "Secrets of Javascript NinJa - 1"
description: ""
date: 2019-06-14
tags: [js, reading]
comments: true
share: true
---
Study notes
---

# C1
## 1.3 Using current best practice
### Debugging

列出各瀏覽器下的各種Debug工具
像是 Firefox 的 Firebug or Chrome 的 dev-tool 等

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

爲了得到更精確的 performance 數據，其實可以多跑幾次，得到合理值。

# C2
## The life cycle overview
1. 使用者輸入網址(URL)
2. 瀏覽器產生請求給伺服器
3. 伺服器執行收到請求，產生相對應的Response給client
4. 瀏覽器開始處理html, css, javascript並開始建構頁面結果 (page building)
5. 產生event queue,一次處理其中一個事件
6. 使用者操作頁面
7. 瀏覽器負責事件處理知道使用者把網頁關掉



![image-20190614115456586](/Users/liuchienwen/Projects/MarkWit/images/image-20190614115456586.png)



## The page building phase



HTML只是瀏覽器拿來建構DOM的藍圖而已，拿到HTML後，開始照著上面的程式碼, 一個一個建立節點，最上面的是HTML，每個節點都可以有很多小孩。

下圖是建立的對照圖。

![image-20190614115937301](/Users/liuchienwen/Library/Application Support/typora-user-images/image-20190614115937301.png)



既然HTML只是藍圖，最後還是會由瀏覽器來Parse並 Construct DOM, 藍圖還是有可能會出錯，當出錯的時候，聰明的瀏覽器也會自動幫忙更正。

## Executing Javascript code
在script這個元素內的Js Code會讓browser的js engine執行。
瀏覽器提供的全域變數，就是window這個物件，browser API可以透過這個來取得，在window下最重要的就是document這個object，它代表這頁DOM，所以可以透過Js來操作這個document的物件來改變DOM。


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

當browser在building page phase時，解析到script tag內的global code，此時js engine會立即執行這段code，而暫停construct DOM，一直到執行到最後一行js code完畢，才會繼續建造節點。只要有還沒處理完的HTML元素，還有還沒有執行完的Js code, 這兩個Steps會交替進行。

1. Construct HTML to DOM
2. Execute Javascript Code

## Event handling

Browser 的 execution environment 一次只執行一行code, 是 single-threaded execution model。

用櫃檯做比喻，櫃檯一次只處理一個客戶所帶來的任務，其他人都要排隊。因爲客人不總是會耐心等候，所以需要一種方式來追蹤已經領號碼牌但是還沒被處理的客人。Js用event queue來處理這個事件。

所有已經發生的事件，像是滑鼠event or keyboard event，或其他用戶產生的Event,都會被放到event queue中，以瀏覽器偵測到event的順序排序。

1. 瀏覽器看event queue 的頭
2. 如果沒有event, browser持續偵測
3. 如果有Event, 如果已經有註冊的event handler, browser會執行這個handler, 執行handler的時候其他events就繼續等著被處理。
   
因爲一次只有一個event被處理，所以如果handler需要花很多時間執行，就有可能造成block現象。

### Event是非同步的
總共有這幾種Event
1. Browser events, like page load...
2. Network events, like response coming...
3. User events, like mouse click ...
4. Timer events, like timeout expires...

### Event Handler
有兩種註冊 Event 的方式，
1. 把 event 發生要呼叫的 function Assign 給某些 property 。書中不建議這個方式，因爲全域變數的關係，指派的function容易被複寫。
  
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