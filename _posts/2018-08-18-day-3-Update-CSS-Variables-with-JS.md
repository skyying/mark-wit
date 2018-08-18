---
layout: post
title: "Day 3 Update CSS Variables with JS"
description: "原來不用sass也可以設定CSS的變數阿！"
date: 2018-08-18
tags: [javascript, javascript30]
comments: true
share: true
---

---

<br>
🥁 [Demo](https://skyying.github.io/Javascript-30/01%20-%20JavaScript%20Drum%20Kit/index-START.html), [Code](https://github.com/skyying/Javascript-30/tree/master/01%20-%20JavaScript%20Drum%20Kit)

## 1. 設定css的變數



不是只有sass才能設定CSS的變數，原來CSS自己本身就有提供設定變數的功能。

```css
// 在頁面的最上層宣告變數
:root {
   --base: #ffffff;
   --spacing: 16px;
   --sizing: 20px;
}
```



#### 宣告

宣告的方式類似定義css的屬性，但需於變數名稱前方加上`--`;

如`--sizing: 16px;`



#### 引用

引用這個變數了，引用的方式如下

`property: var(--variable);`

```
.el {
    background: var(--base);
    padding: var(--spacing);
    filter: blur(var(--sizing));
}
```



## 2. 利用Dataset取得dom element的相關資料

可以在html element上這樣設定相關的資料

```html
<input data-name="sizing" value=0 data-sizing="px"/>
```



如何取用？javascript 提供一個方法來取得以`data-`爲開頭的attribute的值，在`data-`的後面可以直接設定其他名稱，然後透過`element.dataset.othername`來取值。範例如下。



```javascript
let input = document.querySelector("input");

console.log(input.dataset.name) // sizing;

```

只要用`element.dataset.name`的方式，就可以取得當初在html `data-name`屬性設定的值了。



#### 相關資料

1. [using data attributes](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_data_attributes) 

2. [HTMLElement dataset](https://developer.mozilla.org/zh-TW/docs/Web/API/HTMLElement/dataset)

   
