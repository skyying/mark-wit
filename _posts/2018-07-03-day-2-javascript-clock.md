---
layout: post
title: "Day 2 Javascript Clock"
description: "第二天，挑戰用javascript實作一個時鐘吧"
date: 2018-07-03
tags: [javascript, javascript30]
comments: true
share: true
---

---

🕰 [Demo](https://skyying.github.io/Javascript-30/02%20-%20JS%20and%20CSS%20Clock/index-START.html), [Code](https://github.com/skyying/Javascript-30/tree/master/02%20-%20JS%20and%20CSS%20Clock)


這次用`Javascript`來實作類比時鐘，需要的步驟如下
1. 取得正確的時間，並換算出這個時間對應的旋轉角度。
2. 每秒一次，更新時間。

<br>

## 1. Get correct time

Javascript 的date method有很多，但這裏只需要用到3個。

先創造一個 time 的instance, 

```javascript
let t = new Date();
```

接着取得這個 date instance 的小時，分鐘，秒數各是多少？

```javascript

let hour = t.getHours();        //  return 0 - 23
let min = t.getMinutes();      // return 0 - 59
let second = t.getSeconds();  //  return 0 - 59

```


<br>

## 2. Get correct angle for hands

爲這些指針換算正確的旋轉角度。

#### 小時的換算 

360是一圈的角度，要特別注意，類比時鐘是12小時的。`360 / 12 * (hour % 12)`, 最後由於css transform 的 0 度約是在9點鐘的位置，因此，所有換算好的角度都得再加上90度。


#### 分鐘和秒數的換算

`360 / 60 * (min or second)`


## How to rotate an element

利用css的transform來讓指針旋轉。

transform 支援許多屬性，像是scale, translate, skew, perspective,

這裏我們要對這些指針的DOM element設定css transform的角度。

隨著每更新秒，重新取得時間並爲這些dom element 跟新新的角度。

#### 先調整指針旋轉的起始點。

```css
transform-origin: 100%;

```

#### 每秒更新角度


```javascript

//取得這些指針的DOM element
let secondHand = document.querySelector(".second-hand");
let hourHand = document.querySelector(".hour-hand");
let minHand = document.querySelector(".min-hand");

//對指定物件設定傳進來的角度
function setAngle(target, degree) {
    target.style.transform = `rotate(${degree + 90}deg)`;
}

//取得最新時間，並換算角度
function setTime() {
    let d = new Date();
    setAngle(secondHand, 6 * d.getSeconds());
    setAngle(hourHand, 15 * (d.getHours() % 12));
    setAngle(minHand, 6 * d.getMinutes());
}

setInterval(setTime, 1000);


```










