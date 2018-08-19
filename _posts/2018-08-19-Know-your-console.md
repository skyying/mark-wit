---
layout: post
title: "你所不知道的console!!"
description: "介紹除了console.log之外的其他console功能"
date: 2018-08-19
tags: [javascript, javascript30]
comments: true
share: true
---

---

平常最常用的還是console.log，但是在Javascript 30的第9集，就介紹了各種console的用法。

<br>
#### 1. console.log(anything);
第一個就是console.log(), 跨號內可以放任何想要印出來的東西。

```
console.log("hello");
// hello
```

<br>

#### 2. 可以把變數放進console.log() 內

```
console.log("my name is %s", "john");
// my name is john

let name = "helen";
console.log(`my name is ${name}`);
// my name is helen
```

<br>

#### 3. Style your console.log()

原來也可以替console.log()內要印出的東西加上樣式

```
console.log("%c here is som text", "font-size: 15px;");

// here is some text
```

![image-20180819114152431](/images/image-20180819114152431.png)

<br>

#### 4. Warning

也可以設定警告訊息，印出來的console前面會有個警告符號。

```
console.warn("this is a warning");
```

![image-20180819114445681](/images/image-20180819114445681.png)

<br>

#### 5. Error

錯誤提示也可以透過console.error()來設定。

```
console.error("this is wrong");
```

![image-20180819114629870](/images/image-20180819114629870.png)



<br>

#### 6. Info

訊息類的可以用console.info()來設定，印出來的console前面會有一個小的訊息符號。

```
console.info("this is information");
```

![image-20180819114930580](/images/image-20180819114930580.png)



<br>

#### 7. Assert

如果想要驗證一些功能是否正確，可以用console.assert(); 這個功能只有在傳入的值等於`false`時，才會印出來。



```
console.asser(1===1, "1 is not equal to 1");
```

對於上面的這個log是完全不會被印出來的，因爲，1永遠等於1，但如果，改成下面這樣

```
console.assert(1===2, "this is wrong");
// this is wrong
```

就會印出"this is wrong",前面放布林值，後面放如果`false`時要印出的字。

![image-20180819115449317](/images/image-20180819115449317.png)

<br>

#### 8. Clear

清楚歷史的console只需要下clear指令

```
console.clear();
```

<br>

#### 9. View Dom element

可以直接放入`console.log(element)`印出，也可以把利用`console.dir(element)`印出詳細的element資訊



```
console.log(time);

```

![image-20180819115755197](/images/image-20180819115755197.png)

<br>



#### 10. Console.dir();

```
console.dir(time);
//會印出更多該Element的資訊
```

![image-20180819115911720](/images/image-20180819115911720.png)



<br>

#### 11. console.count()

如果要計算某個變數執行的次數，可以用這個方法

```
console.count("test");
console.count("test");
console.count("test");
//test: 1
//test: 2
//test: 3
```

![image-20180819120551511](/images/image-20180819120551511.png)

<br>

#### 12. console.time()

這是用來計時，類似碼錶，可以用`console.time( "any name you want" )`但計時的起始點，用`console.timeEnd()`  當結束點，包圍執行範圍，最後就會印出從起點到結束的時間

```
console.time("fetch data");
fetch(url).then(data=> data.json).then(data=>
console.timeEnd("fetch data");
);

// fetch data: 75.711ms
```



